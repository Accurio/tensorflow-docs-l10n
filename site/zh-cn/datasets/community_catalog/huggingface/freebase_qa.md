# freebase_qa

参考：

- [代码](https://github.com/huggingface/datasets/blob/master/datasets/freebase_qa)
- [Huggingface](https://huggingface.co/datasets/freebase_qa)

使用以下命令在 TFDS 中加载此数据集：

```python
ds = tfds.load('huggingface:freebase_qa')
```

- **说明**：

```
FreebaseQA is for open-domain factoid question answering (QA) tasks over structured knowledge bases, like Freebase The data set is generated by matching trivia-type question-answer pairs with subject-predicateobject triples in Freebase.
```

- **许可**：无已知许可
- **版本**：1.0.0
- **拆分**：

拆分 | 样本
:-- | --:
`'test'` | 3996
`'train'` | 20358
`'validation'` | 3994

- **特征**：

```json
{
    "Question-ID": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "RawQuestion": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "ProcessedQuestion": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "Parses": {
        "feature": {
            "Parse-Id": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "PotentialTopicEntityMention": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "TopicEntityName": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "TopicEntityMid": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "InferentialChain": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "Answers": {
                "feature": {
                    "AnswersMid": {
                        "dtype": "string",
                        "id": null,
                        "_type": "Value"
                    },
                    "AnswersName": {
                        "feature": {
                            "dtype": "string",
                            "id": null,
                            "_type": "Value"
                        },
                        "length": -1,
                        "id": null,
                        "_type": "Sequence"
                    }
                },
                "length": -1,
                "id": null,
                "_type": "Sequence"
            }
        },
        "length": -1,
        "id": null,
        "_type": "Sequence"
    }
}
```
