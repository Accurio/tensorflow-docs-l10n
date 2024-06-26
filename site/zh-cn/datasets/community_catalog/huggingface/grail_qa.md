# grail_qa

参考：

- [代码](https://github.com/huggingface/datasets/blob/master/datasets/grail_qa)
- [Huggingface](https://huggingface.co/datasets/grail_qa)

使用以下命令在 TFDS 中加载此数据集：

```python
ds = tfds.load('huggingface:grail_qa')
```

- **说明**：

```
Strongly Generalizable Question Answering (GrailQA) is a new large-scale, high-quality dataset for question answering on knowledge bases (KBQA) on Freebase with 64,331 questions annotated with both answers and corresponding logical forms in different syntax (i.e., SPARQL, S-expression, etc.). It can be used to test three levels of generalization in KBQA: i.i.d., compositional, and zero-shot.
```

- **许可**：无已知许可
- **版本**：0.0.0
- **拆分**：

拆分 | 样本
:-- | --:
`'test'` | 13231
`'train'` | 44337
`'validation'` | 6763

- **特征**：

```json
{
    "qid": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "question": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "answer": {
        "feature": {
            "answer_type": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "answer_argument": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            },
            "entity_name": {
                "dtype": "string",
                "id": null,
                "_type": "Value"
            }
        },
        "length": -1,
        "id": null,
        "_type": "Sequence"
    },
    "function": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "num_node": {
        "dtype": "int32",
        "id": null,
        "_type": "Value"
    },
    "num_edge": {
        "dtype": "int32",
        "id": null,
        "_type": "Value"
    },
    "graph_query": {
        "nodes": {
            "feature": {
                "nid": {
                    "dtype": "int32",
                    "id": null,
                    "_type": "Value"
                },
                "node_type": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                },
                "id": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                },
                "class": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                },
                "friendly_name": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                },
                "question_node": {
                    "dtype": "int32",
                    "id": null,
                    "_type": "Value"
                },
                "function": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                }
            },
            "length": -1,
            "id": null,
            "_type": "Sequence"
        },
        "edges": {
            "feature": {
                "start": {
                    "dtype": "int32",
                    "id": null,
                    "_type": "Value"
                },
                "end": {
                    "dtype": "int32",
                    "id": null,
                    "_type": "Value"
                },
                "relation": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                },
                "friendly_name": {
                    "dtype": "string",
                    "id": null,
                    "_type": "Value"
                }
            },
            "length": -1,
            "id": null,
            "_type": "Sequence"
        }
    },
    "sparql_query": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "domains": {
        "feature": {
            "dtype": "string",
            "id": null,
            "_type": "Value"
        },
        "length": -1,
        "id": null,
        "_type": "Sequence"
    },
    "level": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    },
    "s_expression": {
        "dtype": "string",
        "id": null,
        "_type": "Value"
    }
}
```
