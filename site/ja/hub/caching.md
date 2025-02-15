# TF Hub からダウンロードしたモデルのキャッシュ

## 概要

`tensorflow_hub` ライブラリでは現在、2 つのモードでモデルをダウンロードすることができます。デフォルトでは、モデルは圧縮アーカイブとしてダウンロードされ、ディスクにキャッシュされます。2 つ目のモードでは、モデルをリモートストレージから TensorFlow に直接読み込むことができます。いずれのモードにおいても、実際の Python コード内の `tensorflow_hub` 関数は、モデルの正規の tfhub.dev URL を使うことができ、使われなければなりません。この URL はシステム間で移植可能で、ドキュメントをナビゲーションしながら閲覧することができます。ユーザーコードで実際のファイルシステムの場所が必要となる（モデルのダウンロードと解凍後、またはモデルのハンドルをファイルシステムのパスに解決した後）ような稀なケースでは、関数 `hub.resolve(handle)` でその場所を取得することができます。

### 圧縮されたダウンロードのキャッシュ

`tensorflow_hub` ライブラリは、モデルが tfhub.dev（またはその他の[ホスティングサイト](hosting.md)）からダウンロードされて解凍されている場合、デフォルトでモデルをファイルシステムにキャッシュします。これは、ディスクの空き容量がわずかでも、ネットワーク帯域幅とレイテンシが非常に優れている場合を除き、ほとんどの環境に推奨されるモードです。

デフォルトのダウンロード場所はローカルの一時ディレクトリですが、環境変数 `TFHUB_CACHE_DIR` を設定する（推奨）か、コマンドラインのフラグ `--tfhub_cache_dir` を渡すことで、カスタマイズすることができます。デフォルトのキャッシュ場所である `/tmp/tfhub_modules`（または  `os.path.join(tempfile.gettempdir(), "tfhub_modules")` が評価した場所）はほとんどの場合に適切です。

システムを再起動後も永続的なキャッシュを利用したいユーザーは、代わりに `TFHUB_CACHE_DIR` をホームディレクトリ内の場所に設定できます。たとえば、Linux システムで bash シェルを使用している場合は、次のような行を `~/.bashrc` に追加できます。

```bash
export TFHUB_CACHE_DIR=$HOME/.cache/tfhub_modules
```

そしてシェルを再起動すると、この場所が使用されるようになります。永続的な場所を使用する場合は、自動クリーンアップが行われないことに注意してください。

### リモートストレージからの読み取り

ユーザーは、モデルをローカルにダウンロードする代わりに、リモートストレージ（GCS）から直接読み取るように `tensorflow_hub` ライブラリに指示することができます。これは次のようにして行います。

```shell
os.environ["TFHUB_MODEL_LOAD_FORMAT"] = "UNCOMPRESSED"
```

または、コマンドラインのフラグ `--tfhub_model_load_format` を `UNCOMPRESSED` に設定しても指示できます。このようにするとキャッシュディレクトリが不要になるため、特に、ディスクの空き容量がわずかしかなくても、高速インターネットに接続できる環境に有効です。

### Colab ノートブックで TPU 実行する

[colab.research.google.com](https://colab.research.google.com) では、計算ワークロードがデフォルトでキャッシュ場所にアクセスできない別のマシンにデリゲートされているため、圧縮モデルをダウンロードすると、TPU ランタイムとの競合が発生します。この状況を回避するには、次の 2 つの方法があります。

#### 1) TPU ワーカーがアクセスできる GCS バケットを使用する

最も簡単な解決策は、上記の説明のとおり、TF Hub の GCS バケットからモデルを読み取るように `tensorflow_hub` を指示することです。独自の GCS バケットを使用しているユーザーは、キャッシュ場所としてそのバケットのディレクトリを指定できます。これは次のようにして行います。

```python
import os
os.environ["TFHUB_CACHE_DIR"] = "gs://my-bucket/tfhub-modules-cache"
```

このコードは `tensorflow_hub` ライブラリを呼び出す前に追加してください。

#### 2) すべての読み取りを Colab ホスト経由でリダイレクトする

もう 1 つの回避策は、すべての読み取り（大きな変数であっても）を Colab ホスト経由でリダイレクトすることです。

```python
load_options =
tf.saved_model.LoadOptions(experimental_io_device='/job:localhost')
reloaded_model = hub.load("https://tfhub.dev/...", options=load_options)
```

**注意:** 有効なハンドルについての詳細は、[こちら](tf2_saved_model.md#model_handles)をご覧ください。
