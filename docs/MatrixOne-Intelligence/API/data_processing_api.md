# 数据处理相关 API

## 工作流

### 创建工作流

```
POST /byoa/api/v1/index_workflow
```

**输入参数：**
  
|  参数                     | 是否必填 |含义       |
| ------------------------- | ------- |---------  |
|  name                    | 是         | 工作流名称  |
|  source_volume_names      | 是       | 原始卷名称 |
|  source_volume_ids        | 是       | 原始卷 id  |
|  target_volume_name        | 是       | 目标卷名称  |
|  target_volume_ids        | 是       | 目标卷 id  |
|  create_target_volume_name| 否       | 新建目标卷名称  |
|  process_mode             | 是       | 处理模式，interval：0:一次处理；1:5 分钟；2:10 分钟；3:30 分钟；4:1 小时；5:2 小时；6:4 小时；7:6 小时；8:8 小时；9：一天；   |
|  file_types               | 是       | 文件类型，目前仅支持 2，为 pdf 类型 |
|  workflow                 | 是       | 工作流，split_length：分段最大长度，最小为 100，最大为 2000；文本预处理规则：remove_empty_lines：true 示表示替换掉连续的空格、换行符和制表符，remove_extra_whitespaces：true 时表示删除所有的 URL 和电子邮箱地址。 |

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow" 

headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "dea010be-1a50-413a-aa7e-e0611a491cab-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin",
}

body = {
    "name":"wf-3",
    "source_volume_names":[
        "b-vol1"
    ],
    "source_volume_ids":[
        "1889223879880048640"
    ],
    "target_volume_name":"a-vol1",
    "target_volume_id":"eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
    "create_target_volume_name":"",
    "process_mode":{
        "interval":0,
        "offset":0
    },
    "file_types":[
        2
    ],
    "workflow":{
        "components":[
            {
                "name":"DocumentCleaner",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner_1739377283742",
                "intro":"DocumentCleaner",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentCleaner-ImageCaption",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner-ImageCaption_1739377283742",
                "intro":"DocumentCleaner-ImageCaption",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentCleaner-ImageOCR",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner-ImageOCR_1739377283742",
                "intro":"DocumentCleaner-ImageOCR",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentEmbedder",
                "type":"haystack.components.embedders.openai_document_embedder.OpenAIDocumentEmbedder",
                "component_id":"DocumentEmbedder_1739377283742",
                "intro":"DocumentEmbedder",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "api_base_url":"https://api.siliconflow.cn/v1",
                    "api_key":{
                        "env_vars":[
                            "OPENAI_API_KEY"
                        ],
                        "strict":"true",
                        "type":"env_var"
                    },
                    "batch_size":32,
                    "dimensions":"null",
                    "embedding_separator":"\n",
                    "meta_fields_to_embed":[

                    ],
                    "model":"BAAI/bge-m3",
                    "organization":"null",
                    "prefix":"",
                    "progress_bar":"true",
                    "suffix":""
                }
            },
            {
                "name":"DocumentJoiner",
                "type":"haystack.components.joiners.document_joiner.DocumentJoiner",
                "component_id":"DocumentJoiner_1739377283742",
                "intro":"DocumentJoiner",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "join_mode":"concatenate",
                    "sort_by_score":"true",
                    "top_k":"null",
                    "weights":"null"
                }
            },
            {
                "name":"DocumentJoiner-Result",
                "type":"haystack.components.joiners.document_joiner.DocumentJoiner",
                "component_id":"DocumentJoiner-Result_1739377283742",
                "intro":"DocumentJoiner-Result",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "join_mode":"concatenate",
                    "sort_by_score":"true",
                    "top_k":"null",
                    "weights":"null"
                }
            },
            {
                "name":"DocumentSplitter",
                "type":"haystack.components.preprocessors.document_splitter.DocumentSplitter",
                "component_id":"DocumentSplitter_1739377283742",
                "intro":"DocumentSplitter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "split_by":"word",
                    "split_length":800,
                    "split_overlap":200,
                    "split_threshold":0
                }
            },
            {
                "name":"DocumentWriter",
                "type":"haystack.components.writers.document_writer.DocumentWriter",
                "component_id":"DocumentWriter_1739377283742",
                "intro":"DocumentWriter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "document_store":{
                        "init_parameters":{
                            "connection_string":{
                                "env_vars":[
                                    "DATABASE_SYNC_URI"
                                ],
                                "strict":"true",
                                "type":"env_var"
                            },
                            "embedding_dimension":1024,
                            "keyword_index_name":"haystack_keyword_index",
                            "recreate_table":"true",
                            "table_name":"embedding_results",
                            "vector_function":"cosine_similarity"
                        },
                        "type":"byoa.integrations.document_stores.mo_document_store.MOIDocumentStore"
                    },
                    "policy":"NONE"
                }
            },
            {
                "name":"FileRouterComponent",
                "type":"haystack.components.routers.file_type_router.FileTypeRouter",
                "component_id":"FileRouterComponent_1739377283742",
                "intro":"FileRouterComponent",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "additional_mimetypes":"null",
                    "mime_types":[
                        "text/plain",
                        "text/markdown",
                        "image/.*",
                        "application/pdf"
                    ]
                }
            },
            {
                "name":"ImageCaptionToDocument",
                "type":"byoa.integrations.components.converters.image_caption_to_document.ImageCaptionToDocument",
                "component_id":"ImageCaptionToDocument_1739377283742",
                "intro":"ImageCaptionToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"ImageOCRToDocument",
                "type":"byoa.integrations.components.converters.image_ocr_to_document.ImageOCRToDocument",
                "component_id":"ImageOCRToDocument_1739377283742",
                "intro":"ImageOCRToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "model":"ucaslcl/GOT-OCR2_0",
                    "tokenizer":"stepfun-ai/GOT-OCR2_0"
                }
            },
            {
                "name":"ImageToDocument",
                "type":"byoa.integrations.components.converters.image_to_document.ImageToDocument",
                "component_id":"ImageToDocument_1739377283742",
                "intro":"ImageToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"MagicPDFToDocument",
                "type":"byoa.integrations.components.converters.magic_pdf_to_document.MagicPDFToDocument",
                "component_id":"MagicPDFToDocument_1739377283742",
                "intro":"MagicPDFToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"MarkdownToDocument",
                "type":"haystack.components.converters.markdown.MarkdownToDocument",
                "component_id":"MarkdownToDocument_1739377283742",
                "intro":"MarkdownToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "progress_bar":"false",
                    "table_to_single_line":"false"
                }
            },
            {
                "name":"MetadataRouter",
                "type":"haystack.components.routers.metadata_router.MetadataRouter",
                "component_id":"MetadataRouter_1739377283742",
                "intro":"MetadataRouter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "rules":{
                        "image":{
                            "conditions":[
                                {
                                    "field":"meta.content_type",
                                    "operator":"==",
                                    "value":"image"
                                }
                            ],
                            "operator":"AND"
                        },
                        "text":{
                            "conditions":[
                                {
                                    "field":"meta.content_type",
                                    "operator":"==",
                                    "value":"text"
                                }
                            ],
                            "operator":"AND"
                        }
                    }
                }
            },
            {
                "name":"PythonExecutor",
                "component_id":"PythonExecutor_1739377283742",
                "intro":"PythonExecutor",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "python_code":""
                },
                "type":"byoa.integrations.components.python_executor.PythonExecutor"
            },
            {
                "name":"TextFileToDocument",
                "type":"haystack.components.converters.txt.TextFileToDocument",
                "component_id":"TextFileToDocument_1739377283742",
                "intro":"TextFileToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "encoding":"utf8"
                }
            }
        ],
        "connections":[
            {
                "receiver":"TextFileToDocument.sources",
                "sender":"FileRouterComponent.text/plain"
            },
            {
                "receiver":"MarkdownToDocument.sources",
                "sender":"FileRouterComponent.text/markdown"
            },
            {
                "receiver":"ImageToDocument.sources",
                "sender":"FileRouterComponent.image/.*"
            },
            {
                "receiver":"MagicPDFToDocument.sources",
                "sender":"FileRouterComponent.application/pdf"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"TextFileToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"MarkdownToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"MagicPDFToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"ImageToDocument.documents"
            },
            {
                "receiver":"MetadataRouter.documents",
                "sender":"DocumentJoiner.documents"
            },
            {
                "receiver":"DocumentCleaner.documents",
                "sender":"MetadataRouter.text"
            },
            {
                "receiver":"ImageOCRToDocument.documents",
                "sender":"MetadataRouter.image"
            },
            {
                "receiver":"ImageCaptionToDocument.documents",
                "sender":"MetadataRouter.image"
            },
            {
                "receiver":"DocumentSplitter.documents",
                "sender":"DocumentCleaner.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentSplitter.documents"
            },
            {
                "receiver":"DocumentCleaner-ImageOCR.documents",
                "sender":"ImageOCRToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentCleaner-ImageOCR.documents"
            },
            {
                "receiver":"DocumentCleaner-ImageCaption.documents",
                "sender":"ImageCaptionToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentCleaner-ImageCaption.documents"
            },
            {
                "receiver":"PythonExecutor.documents",
                "sender":"DocumentJoiner-Result.documents"
            },
            {
                "receiver":"DocumentEmbedder.documents",
                "sender":"PythonExecutor.documents"
            },
            {
                "receiver":"DocumentWriter.documents",
                "sender":"DocumentEmbedder.documents"
            }
        ],
        "edges":[

        ],
        "extra_components":[

        ]
    }
}

response = requests.post(url, json=body, headers=headers)

print(response.json()) 
```

返回：

```bash
{'code': 'ok', 'msg': 'ok', 'data': None}
```

### 查看工作流列表

```
 GET /byoa/api/v1/index_workflow
```

**示例：**

```python
import requests
import json
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow"
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "d252447b-7f1d-4fd4-8b70-9bc2dd5cd505-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}

response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回：

```bash
Response Body: {
    "code": "ok",
    "msg": "ok",
    "data": {
        "total": 1,
        "workflows": [
            {
                "id": "a029a904-1e1c-41af-b361-b6578c92a437",
                "job_meta_id": "53d99056-b7b8-4d9e-baf1-3d3bca24d4f3",
                "name": "wf-1",
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "source_volume_names": [
                    "b-vol1"
                ],
                "file_types": [
                    2
                ],
                "created_at": 1739377287000,
                "creator": "admin",
                "updated_at": 1739377755000,
                "modifier": "admin",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "target_volume_name": "a-vol1",
                "process_mode": {
                    "interval": 0,
                    "offset": 0
                },
                "status": 2
            }
        ]
    }
}
```

### 查看工作流详情

```
GET /byoa/api/v1/index_workflow/{workflow_id}
```

**输出参数：**
  
|  参数             | 含义 |
|  --------------- | ----  |
| id               |工作流 id      |
| name             | 工作流名称    |
| job_meta_id      | 作业元数据 id   |
| source_volume_ids       | 源数据卷列表    |
| source_volume_names       | 源数据卷列表    |
| file_types         | 文件类型列表    |
| created_at       | 创建时间    |
| creator         | 创建人    |
| updated_at         | 更新时间    |
| modifier         | 更新者    |
| target_volume_id         | 目标数据卷 id   |
| target_volume_name | 目标数据卷名   |
| process_mode           | 处理模式   |
| status            | 状态  1：运行中；2：完成；3：停止 |
| workflow           | 工作流    |

**示例：**

```python
import requests
import json
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow/ff5d119a-4e94-4968-ac0c-6ef64fcabb6c"
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "181c0bfb-486f-4e55-a4ea-7fa2a5dae4fa-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}
response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回：

```bash
Response Body: {
    "code": "ok",
    "msg": "ok",
    "data": {
        "id": "ff5d119a-4e94-4968-ac0c-6ef64fcabb6c",
        "name": "test-2",
        "job_meta_id": "edd6ffc3-5c96-4a1b-a6ef-01d21fdbb6d0",
        "source_volume_ids": [
            "1889223879880048640"
        ],
        "source_volume_names": [
            "b-vol1"
        ],
        "file_types": [
            2
        ],
        "created_at": 1739435482000,
        "creator": "admin",
        "updated_at": 1739436347000,
        "modifier": "admin",
        "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
        "target_volume_name": "a-vol2",
        "process_mode": {
            "interval": 5,
            "offset": 0
        },
        "status": 1,
        "workflow": {
            "components": [
                {
                    "name": "DocumentCleaner",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "DocumentCleaner_1739435478121",
                    "intro": "DocumentCleaner",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "ascii_only": false,
                        "keep_id": false,
                        "remove_empty_lines": false,
                        "remove_extra_whitespaces": false,
                        "remove_regex": null,
                        "remove_repeated_substrings": false,
                        "remove_substrings": null,
                        "unicode_normalization": null
                    }
                },
                {
                    "name": "DocumentCleaner-ImageCaption",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "DocumentCleaner-ImageCaption_1739435478121",
                    "intro": "DocumentCleaner-ImageCaption",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "ascii_only": false,
                        "keep_id": false,
                        "remove_empty_lines": false,
                        "remove_extra_whitespaces": false,
                        "remove_regex": null,
                        "remove_repeated_substrings": false,
                        "remove_substrings": null,
                        "unicode_normalization": null
                    }
                }
                // 更多组件...
            ],
            "connections": [
                {
                    "receiver": "TextFileToDocument.sources",
                    "sender": "FileRouterComponent.text/plain"
                },
                {
                    "receiver": "MarkdownToDocument.sources",
                    "sender": "FileRouterComponent.text/markdown"
                }
                // 更多连接...
            ],
            "edges": [],
            "extra_components": []
        }
    }
}
```

### 修改工作流

```
POST /byoa/api/v1/index_workflow/{workflow_id}
```

输入参数参考上面的**创建工作流步**。

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow/fef28ca2-175e-4de9-9ac3-f4aa0da5a745"  
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "fa9f114e-77e0-4c23-aa0f-e982a5ec80e2-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}

body = {
    "name":"wf-3",
    "source_volume_names":[
        "b-vol1"
    ],
    "source_volume_ids":[
        "1889223879880048640"
    ],
    "target_volume_name":"a-vol1",
    "target_volume_id":"eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
    "create_target_volume_name":"",
    "process_mode":{
        "interval":0,
        "offset":0
    },
    "file_types":[
        2
    ],
    "workflow":{
        "components":[
            {
                "name":"DocumentCleaner",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner_1739377283742",
                "intro":"DocumentCleaner",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentCleaner-ImageCaption",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner-ImageCaption_1739377283742",
                "intro":"DocumentCleaner-ImageCaption",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentCleaner-ImageOCR",
                "type":"haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id":"DocumentCleaner-ImageOCR_1739377283742",
                "intro":"DocumentCleaner-ImageOCR",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "ascii_only":"false",
                    "keep_id":"false",
                    "remove_empty_lines":"true",
                    "remove_extra_whitespaces":"true",
                    "remove_regex":"([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+)|https?://[^\\s]+",
                    "remove_repeated_substrings":"false",
                    "remove_substrings":"null",
                    "unicode_normalization":"null"
                }
            },
            {
                "name":"DocumentEmbedder",
                "type":"haystack.components.embedders.openai_document_embedder.OpenAIDocumentEmbedder",
                "component_id":"DocumentEmbedder_1739377283742",
                "intro":"DocumentEmbedder",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "api_base_url":"https://api.siliconflow.cn/v1",
                    "api_key":{
                        "env_vars":[
                            "OPENAI_API_KEY"
                        ],
                        "strict":"true",
                        "type":"env_var"
                    },
                    "batch_size":32,
                    "dimensions":"null",
                    "embedding_separator":"\n",
                    "meta_fields_to_embed":[

                    ],
                    "model":"BAAI/bge-m3",
                    "organization":"null",
                    "prefix":"",
                    "progress_bar":"true",
                    "suffix":""
                }
            },
            {
                "name":"DocumentJoiner",
                "type":"haystack.components.joiners.document_joiner.DocumentJoiner",
                "component_id":"DocumentJoiner_1739377283742",
                "intro":"DocumentJoiner",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "join_mode":"concatenate",
                    "sort_by_score":"true",
                    "top_k":"null",
                    "weights":"null"
                }
            },
            {
                "name":"DocumentJoiner-Result",
                "type":"haystack.components.joiners.document_joiner.DocumentJoiner",
                "component_id":"DocumentJoiner-Result_1739377283742",
                "intro":"DocumentJoiner-Result",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "join_mode":"concatenate",
                    "sort_by_score":"true",
                    "top_k":"null",
                    "weights":"null"
                }
            },
            {
                "name":"DocumentSplitter",
                "type":"haystack.components.preprocessors.document_splitter.DocumentSplitter",
                "component_id":"DocumentSplitter_1739377283742",
                "intro":"DocumentSplitter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "split_by":"word",
                    "split_length":800,
                    "split_overlap":200,
                    "split_threshold":0
                }
            },
            {
                "name":"DocumentWriter",
                "type":"haystack.components.writers.document_writer.DocumentWriter",
                "component_id":"DocumentWriter_1739377283742",
                "intro":"DocumentWriter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "document_store":{
                        "init_parameters":{
                            "connection_string":{
                                "env_vars":[
                                    "DATABASE_SYNC_URI"
                                ],
                                "strict":"true",
                                "type":"env_var"
                            },
                            "embedding_dimension":1024,
                            "keyword_index_name":"haystack_keyword_index",
                            "recreate_table":"true",
                            "table_name":"embedding_results",
                            "vector_function":"cosine_similarity"
                        },
                        "type":"byoa.integrations.document_stores.mo_document_store.MOIDocumentStore"
                    },
                    "policy":"NONE"
                }
            },
            {
                "name":"FileRouterComponent",
                "type":"haystack.components.routers.file_type_router.FileTypeRouter",
                "component_id":"FileRouterComponent_1739377283742",
                "intro":"FileRouterComponent",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "additional_mimetypes":"null",
                    "mime_types":[
                        "text/plain",
                        "text/markdown",
                        "image/.*",
                        "application/pdf"
                    ]
                }
            },
            {
                "name":"ImageCaptionToDocument",
                "type":"byoa.integrations.components.converters.image_caption_to_document.ImageCaptionToDocument",
                "component_id":"ImageCaptionToDocument_1739377283742",
                "intro":"ImageCaptionToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"ImageOCRToDocument",
                "type":"byoa.integrations.components.converters.image_ocr_to_document.ImageOCRToDocument",
                "component_id":"ImageOCRToDocument_1739377283742",
                "intro":"ImageOCRToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "model":"ucaslcl/GOT-OCR2_0",
                    "tokenizer":"stepfun-ai/GOT-OCR2_0"
                }
            },
            {
                "name":"ImageToDocument",
                "type":"byoa.integrations.components.converters.image_to_document.ImageToDocument",
                "component_id":"ImageToDocument_1739377283742",
                "intro":"ImageToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"MagicPDFToDocument",
                "type":"byoa.integrations.components.converters.magic_pdf_to_document.MagicPDFToDocument",
                "component_id":"MagicPDFToDocument_1739377283742",
                "intro":"MagicPDFToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{

                }
            },
            {
                "name":"MarkdownToDocument",
                "type":"haystack.components.converters.markdown.MarkdownToDocument",
                "component_id":"MarkdownToDocument_1739377283742",
                "intro":"MarkdownToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "progress_bar":"false",
                    "table_to_single_line":"false"
                }
            },
            {
                "name":"MetadataRouter",
                "type":"haystack.components.routers.metadata_router.MetadataRouter",
                "component_id":"MetadataRouter_1739377283742",
                "intro":"MetadataRouter",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "rules":{
                        "image":{
                            "conditions":[
                                {
                                    "field":"meta.content_type",
                                    "operator":"==",
                                    "value":"image"
                                }
                            ],
                            "operator":"AND"
                        },
                        "text":{
                            "conditions":[
                                {
                                    "field":"meta.content_type",
                                    "operator":"==",
                                    "value":"text"
                                }
                            ],
                            "operator":"AND"
                        }
                    }
                }
            },
            {
                "name":"PythonExecutor",
                "component_id":"PythonExecutor_1739377283742",
                "intro":"PythonExecutor",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "python_code":""
                },
                "type":"byoa.integrations.components.python_executor.PythonExecutor"
            },
            {
                "name":"TextFileToDocument",
                "type":"haystack.components.converters.txt.TextFileToDocument",
                "component_id":"TextFileToDocument_1739377283742",
                "intro":"TextFileToDocument",
                "position":{
                    "x":0,
                    "y":0
                },
                "input_keys":{

                },
                "output_keys":{

                },
                "init_parameters":{
                    "encoding":"utf8"
                }
            }
        ],
        "connections":[
            {
                "receiver":"TextFileToDocument.sources",
                "sender":"FileRouterComponent.text/plain"
            },
            {
                "receiver":"MarkdownToDocument.sources",
                "sender":"FileRouterComponent.text/markdown"
            },
            {
                "receiver":"ImageToDocument.sources",
                "sender":"FileRouterComponent.image/.*"
            },
            {
                "receiver":"MagicPDFToDocument.sources",
                "sender":"FileRouterComponent.application/pdf"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"TextFileToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"MarkdownToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"MagicPDFToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner.documents",
                "sender":"ImageToDocument.documents"
            },
            {
                "receiver":"MetadataRouter.documents",
                "sender":"DocumentJoiner.documents"
            },
            {
                "receiver":"DocumentCleaner.documents",
                "sender":"MetadataRouter.text"
            },
            {
                "receiver":"ImageOCRToDocument.documents",
                "sender":"MetadataRouter.image"
            },
            {
                "receiver":"ImageCaptionToDocument.documents",
                "sender":"MetadataRouter.image"
            },
            {
                "receiver":"DocumentSplitter.documents",
                "sender":"DocumentCleaner.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentSplitter.documents"
            },
            {
                "receiver":"DocumentCleaner-ImageOCR.documents",
                "sender":"ImageOCRToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentCleaner-ImageOCR.documents"
            },
            {
                "receiver":"DocumentCleaner-ImageCaption.documents",
                "sender":"ImageCaptionToDocument.documents"
            },
            {
                "receiver":"DocumentJoiner-Result.documents",
                "sender":"DocumentCleaner-ImageCaption.documents"
            },
            {
                "receiver":"PythonExecutor.documents",
                "sender":"DocumentJoiner-Result.documents"
            },
            {
                "receiver":"DocumentEmbedder.documents",
                "sender":"PythonExecutor.documents"
            },
            {
                "receiver":"DocumentWriter.documents",
                "sender":"DocumentEmbedder.documents"
            }
        ],
        "edges":[

        ],
        "extra_components":[

        ]
    }
}

response = requests.put(url, json=body, headers=headers)
print(response.json()) 
```

返回：

```
{'code': 'ok', 'msg': 'ok', 'data': None}
```

### 删除工作流

```
DELETE /byoa/api/v1/index_workflow/{workflow_id}?[delete_data=true]
```

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow/729e7a03-652d-46e0-bdad-b05ec5b80cea?delete_data=true"

headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "011d4b66-ace5-4d58-88a4-bc76719acda5-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}

response = requests.delete(url, headers=headers)

if response.status_code == 200:
    print(response.json())  
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

返回：

```bash
{'code': 'ok', 'msg': 'ok', 'data': None}
```

## 工作流分支

### 创建工作流分支

```
POST /byoa/api/v1/workflow_meta/{workflow_id}/branch
```

**路径参数：**
*   `workflow_id` (string, 必填): 工作流 ID

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `user-name` (string, 可选): 用户名 (可选)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID
*   `Content-Type` (string, 必填): 通常为 `application/json`

**Body 输入参数 (`WorkflowBranchRequest`)：**

| 参数          | 是否必填 | 类型     | 含义                                                                 |
|---------------|----------|----------|----------------------------------------------------------------------|
| branch_name   | 否       | string   | 分支名 (默认为空)                                                        |
| workflow      | 是       | object   | 工作流配置对象 (结构同创建工作流时的 `workflow` 对象，但应用于此分支) |

**Body 示例 (`WorkflowBranchRequest`)：**

```json
{
    "branch_name": "my-new-branch",
    "workflow": {
        // 此处为完整的 workflow 配置对象，
        // 参考"创建工作流"部分的 workflow 结构。
        // 例如，可以仅修改部分组件参数或连接。
        "components": [
            {
                "name": "DocumentCleaner_Branch",
                "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id": "DocCleaner_Branch_123",
                "intro": "Branch-specific document cleaner",
                "position": {"x": 50, "y": 100},
                "input_keys": {},
                "output_keys": {},
                "init_parameters": {
                    "remove_empty_lines": true,
                    "remove_extra_whitespaces": true
                }
            },
            {
                "name": "DocumentSplitter_Branch",
                "type": "haystack.components.preprocessors.document_splitter.DocumentSplitter",
                "component_id": "DocSplitter_Branch_456",
                "intro": "Branch-specific document splitter",
                "position": {"x": 50, "y": 200},
                "input_keys": {},
                "output_keys": {},
                "init_parameters": {
                    "split_by": "word",
                    "split_length": 300,
                    "split_overlap": 50
                }
            }
        ],
        "connections": [
            {
                "sender": "DocCleaner_Branch_123.documents", // 注意：这里的组件ID应与上面定义的组件ID匹配
                "receiver": "DocSplitter_Branch_456.documents" // 注意：这里的组件ID应与上面定义的组件ID匹配
            }
        ],
        "edges": [],
        "extra_components": []
    }
}
```

**示例：**

```python
import requests
import json

# API URL, 将 {workflow_id} 替换为实际的工作流 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/{workflow_id}/branch"

headers = {
    "user-id": "your_user_id_workspace_id", # 例如 "0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx"
    "user-name": "optional_user_name",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login", # 例如 "fa6467a6-...:admin:accountadmin"
    "Content-Type": "application/json"
}

body = {
    "branch_name": "feature-branch-A",
    "workflow": {
        "components": [
            {
                "name": "DocumentCleaner_Branch_A",
                "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id": "DocCleaner_Branch_A_789",
                "intro": "Branch A document cleaner",
                "position": {"x": 50, "y": 100},
                "input_keys": {},
                "output_keys": {},
                "init_parameters": {
                    "remove_empty_lines": false,
                    "remove_extra_whitespaces": true
                }
            }
        ], 
        "connections": [],
        "edges": [],
        "extra_components": []
    }
}

response = requests.post(url.replace("{workflow_id}", "actual_workflow_id_here"), json=body, headers=headers)

if response.status_code == 200:
    print(response.json())
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`NoneDataResp`)：**

```json
{
    "code": "ok",
    "msg": "ok",
    "data": null
}
```

### 查看工作流分支列表

```
GET /byoa/api/v1/workflow_meta/{workflow_id}/branch
```

**路径参数：**
*   `workflow_id` (string, 必填): 工作流 ID

**Query 参数：**
*   `status_in` (array[integer], 可选): 工作流状态 (用于过滤)
*   `branch_status` (array[integer], 可选): 分支状态 (用于过滤)

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID

**(无 Body 输入参数)**

**示例：**

```python
import requests
import json

# API URL, 将 {workflow_id} 替换为实际的工作流 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/{workflow_id}/branch"

headers = {
    "user-id": "your_user_id_workspace_id",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login"
}

# 可选的查询参数
params = {
    # "status_in": [1, 2], # 例如：只看运行中和已完成的
    # "branch_status": [0]  # 例如：只看某种状态的分支
}

response = requests.get(url.replace("{workflow_id}", "actual_workflow_id_here"), headers=headers, params=params)

if response.status_code == 200:
    print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`MOIResponse_WorkflowListResponse_` -> `WorkflowListResponse` -> `workflows`: array of `WorkflowListItem`)：**

```json
{
    "code": "ok",
    "msg": "ok",
    "data": {
        "total": 1, // 分支总数
        "workflows": [ // 注意：虽然字段名是 workflows，但这里是分支列表
            {
                "id": "workflow_id_parent", // 父工作流ID
                "name": "Parent Workflow Name",
                "created_at": 1678886400000,
                "creator": "admin",
                "updated_at": 1678886400000,
                "modifier": "admin",
                "source_volume_ids": ["vol_id_1"],
                "source_volume_names": ["source_volume_A"],
                "file_types": [2],
                "target_volume_id": "target_vol_parent",
                "target_volume_name": "target_vol_name_parent",
                "process_mode": {"interval": 0, "offset": 0},
                "status": 1, // 父工作流状态
                "version": "1",
                "branch_id": "branch_id_example_123", // 分支ID
                "branch_name": "feature-branch-A",    // 分支名
                "branch_status": 0,                   // 分支状态
                "branch_volume_id": "target_vol_branch_A" // 分支目标数据卷ID
            }
        ]
    }
}
```

### 获取工作流分支详情

```
GET /byoa/api/v1/workflow_meta/branch/{branch_id}
```

**路径参数：**
*   `branch_id` (string, 必填): 工作流-分支ID

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID

**(无 Body 输入参数)**

**示例：**

```python
import requests
import json

# API URL, 将 {branch_id} 替换为实际的分支 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/branch/{branch_id}"

headers = {
    "user-id": "your_user_id_workspace_id",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login"
}

response = requests.get(url.replace("{branch_id}", "actual_branch_id_here"), headers=headers)

if response.status_code == 200:
    print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`MOIResponse_WorkflowDetailResponse_` -> `WorkflowDetailResponse`)：**
返回的是包含该分支信息的父工作流的详细信息。

```json
{
    "code": "ok",
    "msg": "ok",
    "data": {
        "id": "parent_workflow_id", // 父工作流ID
        "name": "Parent Workflow Name",
        "source_volume_ids": ["vol_id_1"],
        "source_volume_names": ["source_volume_A"],
        "target_volume_id": "parent_target_vol_id", // 父工作流的目标卷
        "target_volume_name": "parent_target_vol_name",
        "file_types": [2],
        "process_mode": {"interval": 0, "offset": 0},
        "priority": 300,
        "created_at": 1678886400000,
        "creator": "admin",
        "updated_at": 1678886500000,
        "modifier": "admin",
        "status": 1, // 父工作流状态
        "workflow": {
            // 父工作流的配置 (如果分支未覆盖，则与分支配置相同)
            "components": [ /* ... */ ],
            "connections": [ /* ... */ ],
            "edges": [],
            "extra_components": []
        },
        "branch_id": "actual_branch_id_here", // 当前分支的ID
        "branch_name": "feature-branch-A",   // 当前分支的名称
        "branch_status": 0,                  // 当前分支的状态
        "branch_volume_id": "branch_target_vol_id", // 当前分支的目标卷ID
        "version": "1.1-branchA", // 可能有版本信息
        "branches": [ // 父工作流下的所有分支列表 (可选，取决于API实现)
            {
                "branch_id": "actual_branch_id_here",
                "branch_name": "feature-branch-A",
                // ...other branch metadata...
                "workflow": { /* 该分支的特定workflow配置 */ }
            }
            // ...
        ]
    }
}
```

### 更新工作流分支

```
PUT /byoa/api/v1/workflow_meta/branch/{branch_id}
```

**路径参数：**
*   `branch_id` (string, 必填): 工作流-分支ID

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `user-name` (string, 可选): 用户名 (可选)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID
*   `Content-Type` (string, 必填): 通常为 `application/json`

**Body 输入参数 (`UpdateWorkflowBranchRequest`)：**

| 参数        | 是否必填 | 类型   | 含义                                                               | 
|-------------|----------|--------|--------------------------------------------------------------------|
| branch_name | 否       | string | 新的分支名                                                           |
| workflow    | 是       | object | 更新后的工作流配置对象 (结构同创建工作流时的 `workflow` 对象) |

**Body 示例 (`UpdateWorkflowBranchRequest`)：**

```json
{
    "branch_name": "my-updated-branch-name",
    "workflow": {
        // 此处为更新后的完整 workflow 配置对象
        // 参考"创建工作流"部分的 workflow 结构。
        "components": [
             {
                "name": "DocumentSplitter",
                "type": "haystack.components.preprocessors.document_splitter.DocumentSplitter",
                "component_id": "DocSplitter_Branch_XYZ_Updated", 
                "intro": "DocumentSplitter for updated branch",
                "position": {"x":0,"y":0},
                "input_keys":{},
                "output_keys":{},
                "init_parameters":{
                    "split_by":"sentence",
                    "split_length":10, 
                    "split_overlap":2,
                    "split_threshold":0
                }
            }
        ],
        "connections": [
        ],
        "edges": [],
        "extra_components": []
    }
}
```

**示例：**

```python
import requests
import json

# API URL, 将 {branch_id} 替换为实际的分支 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/branch/{branch_id}"

headers = {
    "user-id": "your_user_id_workspace_id",
    "user-name": "optional_user_name",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login",
    "Content-Type": "application/json"
}

body = {
    "branch_name": "feature-branch-A-updated",
    "workflow": {
        "components": [
            {
                "name": "DocumentCleaner_Branch_A_Updated",
                "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                "component_id": "DocCleaner_Branch_A_789_Updated",
                "intro": "Branch A document cleaner - updated",
                "position": {"x": 50, "y": 150},
                "input_keys": {},
                "output_keys": {},
                "init_parameters": {
                    "remove_empty_lines": true,
                    "remove_extra_whitespaces": false,
                    "remove_regex": "(https?://\\S+)"
                }
            }
        ],
        "connections": [],
        "edges": [],
        "extra_components": []
    }
}

response = requests.put(url.replace("{branch_id}", "actual_branch_id_here"), json=body, headers=headers)

if response.status_code == 200:
    print(response.json())
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`NoneDataResp`)：**

```json
{
    "code": "ok",
    "msg": "ok",
    "data": null
}
```

### 删除工作流分支

```
DELETE /byoa/api/v1/workflow_meta/branch/{branch_id}
```

**路径参数：**
*   `branch_id` (string, 必填): 工作流-分支ID

**Query 参数：**
*   `delete_data` (boolean, 可选): 是否删除分支产生的数据 (默认: false)

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID

**(无 Body 输入参数)**

**示例：**

```python
import requests
import json

# API URL, 将 {branch_id} 替换为实际的分支 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/branch/{branch_id}"

headers = {
    "user-id": "your_user_id_workspace_id",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login"
}

# 可选的查询参数
params = {
    "delete_data": True # 或 False
}

response = requests.delete(url.replace("{branch_id}", "actual_branch_id_here"), headers=headers, params=params)

if response.status_code == 200: # OpenAPI 可能返回 200 带有 NoneDataResp，或者 204 No Content
    try:
        print(response.json())
    except json.JSONDecodeError:
        print("请求成功，无返回内容 (可能为 204 No Content)")
elif response.status_code == 204:
    print("请求成功，资源已删除 (204 No Content)")
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`NoneDataResp` 或 HTTP 204 No Content)：**

```json
{
    "code": "ok",
    "msg": "ok",
    "data": null
}
```

### 启用工作流分支

```
PUT /byoa/api/v1/workflow_meta/branch/{branch_id}/enable
```

**路径参数：**
*   `branch_id` (string, 必填): 工作流-分支ID

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID
*   `Content-Type` (string, 必填): 通常为 `application/json`

**(无 Body 输入参数)**

**示例：**

```python
import requests
import json

# API URL, 将 {branch_id} 替换为实际的分支 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/branch/{branch_id}/enable"

headers = {
    "user-id": "your_user_id_workspace_id",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login",
    "Content-Type": "application/json" # 通常 PUT 请求需要指定 Content-Type，即使 body 为空
}

# 此接口通常没有请求体

response = requests.put(url.replace("{branch_id}", "actual_branch_id_here"), headers=headers)

if response.status_code == 200:
    print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`MOIResponse_WorkflowDetailResponse_`)：**
返回启用后的分支详情（结构同"获取工作流分支详情"的返回）。

```json
{
    "code": "ok",
    "msg": "ok",
    "data": {
        // ... 工作流及分支详细信息 ...
        "id": "parent_workflow_id_for_enable",
        "name": "WorkflowForEnable",
        "source_volume_ids": ["src_vol_enable"],
        "source_volume_names": ["Source Volume Enable"],
        "target_volume_id": "tgt_vol_enable_parent",
        "target_volume_name": "Target Volume Enable Parent",
        "file_types": [2, 6],
        "process_mode": {"interval": 60, "offset": 5},
        "priority": 200,
        "created_at": 1678887000000,
        "creator": "enable_user",
        "updated_at": 1678887050000,
        "modifier": "enable_user",
        "status": 1,        
        "workflow": {
             "components": [
                {
                    "name": "EnableBranchCleaner",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "EnableCleaner001",
                    "intro": "Cleaner for enable branch test",
                    "position": {"x":0,"y":0},
                    "input_keys":{},
                    "output_keys":{},
                    "init_parameters":{"remove_empty_lines":true}
                }
            ],
            "connections": [],
            "edges": [],
            "extra_components": []
        },
        "branch_id": "actual_branch_id_here",
        "branch_name": "feature-branch-A",
        "branch_status": 1, // 状态变为启用状态 (具体值需参考API定义)
        "branch_volume_id": "branch_vol_for_enable",
        "version": "1.0-branchA-enabled"
    }
}
```

### 禁用工作流分支

```
PUT /byoa/api/v1/workflow_meta/branch/{branch_id}/disable
```

**路径参数：**
*   `branch_id` (string, 必填): 工作流-分支ID

**Header 参数：**
*   `user-id` (string, 必填): 用户ID (工作区 ID)
*   `Access-Token` (string, 必填): 鉴权Token
*   `uid` (string, 必填): 用户登录后获取的UID
*   `Content-Type` (string, 必填): 通常为 `application/json`

**(无 Body 输入参数)**

**示例：**

```python
import requests
import json

# API URL, 将 {branch_id} 替换为实际的分支 ID
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/workflow_meta/branch/{branch_id}/disable"

headers = {
    "user-id": "your_user_id_workspace_id",
    "Access-Token": "your_access_token",
    "uid": "your_uid_from_login",
    "Content-Type": "application/json" # 通常 PUT 请求需要指定 Content-Type
}

# 此接口通常没有请求体

response = requests.put(url.replace("{branch_id}", "actual_branch_id_here"), headers=headers)

if response.status_code == 200:
    print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

**返回 (`MOIResponse_WorkflowDetailResponse_`)：**
返回禁用后的分支详情（结构同"获取工作流分支详情"的返回）。

```json
{
    "code": "ok",
    "msg": "ok",
    "data": {
        // ... 工作流及分支详细信息 ...
        "id": "parent_workflow_id_for_disable",
        "name": "WorkflowForDisable",
        "source_volume_ids": ["src_vol_disable"],
        "source_volume_names": ["Source Volume Disable"],
        "target_volume_id": "tgt_vol_disable_parent",
        "target_volume_name": "Target Volume Disable Parent",
        "file_types": [3],
        "process_mode": {"interval": 0, "offset": 0},
        "priority": 100,
        "created_at": 1678888000000,
        "creator": "disable_user",
        "updated_at": 1678888050000,
        "modifier": "disable_user",
        "status": 2, 
        "workflow": {
             "components": [
                {
                    "name": "DisableBranchSplitter",
                    "type": "haystack.components.preprocessors.document_splitter.DocumentSplitter",
                    "component_id": "DisableSplitter001",
                    "intro": "Splitter for disable branch test",
                    "position": {"x":0,"y":0},
                    "input_keys":{},
                    "output_keys":{},
                    "init_parameters":{"split_length":100}
                }
            ],
            "connections": [],
            "edges": [],
            "extra_components": []
        },
        "branch_id": "actual_branch_id_here",
        "branch_name": "feature-branch-A",
        "branch_status": 2, // 状态变为禁用状态 (具体值需参考API定义)
        "branch_volume_id": "branch_vol_for_disable",
        "version": "1.0-branchA-disabled"
    }
}
```

## 作业

### 查看作业列表

```
GET /byoa/api/v1/index_workflow_job
```

**输出参数：**
  
|  参数             | 含义 |
|  --------------- | ----  |
| id               |作业 id       |
| workflow_name      | 工作流名称     |
| name             | 连接器名称    |
| source_volume_names           | 原始卷名称    |
| source_volume_ids       | 原始卷 id   |
| target_volume_name       | 目标卷名称    |
| target_volume_id         | 目标卷 id    |
| file_types       | 文件类型，2 为 pdf 格式    |
| status         | 工作流状态    |
| workflow_id | 工作流 id  |

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow_job"  
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "011d4b66-ace5-4d58-88a4-bc76719acda5-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}
response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))

```

返回

```bash
Response Body: {
    "code": "ok",
    "msg": "ok",
    "data": {
        "total": 10,
        "jobs": [
            {
                "id": "0194fb2c-f5c5-7d42-8d09-fdc3d8414777",
                "workflow_name": "wf-2",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol2",
                "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T17:20:15.000000+0000",
                "end_time": "2025-02-12T17:20:15.000000+0000",
                "duration": 0,
                "processed_count": 0,
                "total_count": 0,
                "status": 2,
                "workflow_id": "729e7a03-652d-46e0-bdad-b05ec5b80cea",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194fb28-61ae-7aac-8500-a4c924a68211",
                "workflow_name": "wf-4",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol2",
                "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T17:15:15.000000+0000",
                "end_time": "2025-02-12T17:21:17.000000+0000",
                "duration": 362,
                "processed_count": 1,
                "total_count": 1,
                "status": 2,
                "workflow_id": "c6dcbad5-f85d-42b7-942c-2e8d3445a4e6",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194fb28-61af-708a-915e-6f140a2424fe",
                "workflow_name": "wf-2",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol2",
                "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T17:15:15.000000+0000",
                "end_time": "2025-02-12T17:15:15.000000+0000",
                "duration": 0,
                "processed_count": 0,
                "total_count": 0,
                "status": 2,
                "workflow_id": "729e7a03-652d-46e0-bdad-b05ec5b80cea",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194fb23-cd65-767c-b58f-db7c4456b896",
                "workflow_name": "wf-2",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol2",
                "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T17:10:15.000000+0000",
                "end_time": "2025-02-12T17:16:17.000000+0000",
                "duration": 362,
                "processed_count": 1,
                "total_count": 1,
                "status": 2,
                "workflow_id": "729e7a03-652d-46e0-bdad-b05ec5b80cea",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194fb06-8044-70e4-8a54-16f5a0e3c720",
                "workflow_name": "wf-3",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T16:38:15.000000+0000",
                "end_time": "2025-02-12T16:39:16.000000+0000",
                "duration": 61,
                "processed_count": 1,
                "total_count": 1,
                "status": 3,
                "workflow_id": "2c0be55b-af55-4787-baac-3d8e7d987fe7",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194faf7-d9a0-7347-8726-a86f52cf67c7",
                "workflow_name": "wf-1",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-12T16:22:15.000000+0000",
                "end_time": "2025-02-12T16:28:16.000000+0000",
                "duration": 361,
                "processed_count": 1,
                "total_count": 1,
                "status": 2,
                "workflow_id": "a029a904-1e1c-41af-b361-b6578c92a437",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194f423-c2a7-7cc5-87ce-97fa942ac6ce",
                "workflow_name": "wk-3",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-11T08:32:52.000000+0000",
                "end_time": "2025-02-11T08:38:52.000000+0000",
                "duration": 360,
                "processed_count": 1,
                "total_count": 1,
                "status": 2,
                "workflow_id": "4f209aa9-186c-442a-b324-d7eebaca4cd0",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194f41d-59d3-7899-9fa8-24343214df7f",
                "workflow_name": "wf-3",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-11T08:25:52.000000+0000",
                "end_time": "2025-02-11T08:31:52.000000+0000",
                "duration": 360,
                "processed_count": 1,
                "total_count": 1,
                "status": 2,
                "workflow_id": "ea64f8ba-b984-46a3-acb0-628849538244",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194f40f-9da9-7927-890c-4bea252e0235",
                "workflow_name": "wf-2",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-11T08:10:52.000000+0000",
                "end_time": "2025-02-11T08:10:52.000000+0000",
                "duration": 0,
                "processed_count": 0,
                "total_count": 0,
                "status": 2,
                "workflow_id": "d2842368-37dc-4b49-930a-25f16a8fc0c8",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            },
            {
                "id": "0194f40c-deb5-7466-bd7f-7c930a034bcd",
                "workflow_name": "wf-1",
                "source_volume_names": [
                    "b-vol1"
                ],
                "source_volume_ids": [
                    "1889223879880048640"
                ],
                "target_volume_name": "a-vol1",
                "target_volume_id": "eb42f0a1-ab18-4010-b95c-cd1716dd5e95",
                "file_types": [
                    2
                ],
                "start_time": "2025-02-11T08:07:52.000000+0000",
                "end_time": "2025-02-11T08:07:52.000000+0000",
                "duration": 0,
                "processed_count": 0,
                "total_count": 0,
                "status": 2,
                "workflow_id": "f6c0b040-5403-42b9-a914-bbf2935d69f0",
                "workflow": {
                    "components": null,
                    "connections": null,
                    "edges": null,
                    "extra_components": null
                }
            }
        ]
    }
}
```

### 查看作业详情

```
GET /byoa/api/v1/index_workflow_job/{job_id}
```

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow_job/0194fb2c-f5c5-7d42-8d09-fdc3d8414777"
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "a6e11303-f4fd-46c0-b5ff-c774e96f64a3-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}
response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回

```bash
Response Body: {
    "code": "ok",
    "msg": "ok",
    "data": {
        "id": "0194fb2c-f5c5-7d42-8d09-fdc3d8414777",
        "workflow_name": "wf-2",
        "source_volume_names": [
            "b-vol1"
        ],
        "source_volume_ids": [
            "1889223879880048640"
        ],
        "target_volume_name": "a-vol2",
        "target_volume_id": "dbcc0d71-31f9-4799-b404-096f9e8e57f9",
        "file_types": [
            2
        ],
        "start_time": "2025-02-12T17:20:15.000000+0000",
        "end_time": "2025-02-12T17:20:15.000000+0000",
        "duration": 0,
        "processed_count": 0,
        "total_count": 0,
        "status": 2,
        "workflow_id": "729e7a03-652d-46e0-bdad-b05ec5b80cea",
        "workflow": {
            "components": [
                {
                    "name": "DocumentCleaner",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "DocumentCleaner_1739380168023",
                    "intro": "DocumentCleaner",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "ascii_only": false,
                        "keep_id": false,
                        "remove_empty_lines": true,
                        "remove_extra_whitespaces": true,
                        "remove_regex": null,
                        "remove_repeated_substrings": false,
                        "remove_substrings": null,
                        "unicode_normalization": null
                    }
                },
                {
                    "name": "DocumentCleaner-ImageCaption",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "DocumentCleaner-ImageCaption_1739380168023",
                    "intro": "DocumentCleaner-ImageCaption",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "ascii_only": false,
                        "keep_id": false,
                        "remove_empty_lines": true,
                        "remove_extra_whitespaces": true,
                        "remove_regex": null,
                        "remove_repeated_substrings": false,
                        "remove_substrings": null,
                        "unicode_normalization": null
                    }
                },
                {
                    "name": "DocumentCleaner-ImageOCR",
                    "type": "haystack.components.preprocessors.document_cleaner.DocumentCleaner",
                    "component_id": "DocumentCleaner-ImageOCR_1739380168023",
                    "intro": "DocumentCleaner-ImageOCR",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "ascii_only": false,
                        "keep_id": false,
                        "remove_empty_lines": true,
                        "remove_extra_whitespaces": true,
                        "remove_regex": null,
                        "remove_repeated_substrings": false,
                        "remove_substrings": null,
                        "unicode_normalization": null
                    }
                },
                {
                    "name": "DocumentEmbedder",
                    "type": "haystack.components.embedders.openai_document_embedder.OpenAIDocumentEmbedder",
                    "component_id": "DocumentEmbedder_1739380168023",
                    "intro": "DocumentEmbedder",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "api_base_url": "https://api.siliconflow.cn/v1",
                        "api_key": {
                            "env_vars": [
                                "OPENAI_API_KEY"
                            ],
                            "strict": true,
                            "type": "env_var"
                        },
                        "batch_size": 32,
                        "dimensions": null,
                        "embedding_separator": "\n",
                        "meta_fields_to_embed": [],
                        "model": "BAAI/bge-m3",
                        "organization": null,
                        "prefix": "",
                        "progress_bar": true,
                        "suffix": ""
                    }
                },
                {
                    "name": "DocumentJoiner",
                    "type": "haystack.components.joiners.document_joiner.DocumentJoiner",
                    "component_id": "DocumentJoiner_1739380168023",
                    "intro": "DocumentJoiner",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "join_mode": "concatenate",
                        "sort_by_score": true,
                        "top_k": null,
                        "weights": null
                    }
                },
                {
                    "name": "DocumentJoiner-Result",
                    "type": "haystack.components.joiners.document_joiner.DocumentJoiner",
                    "component_id": "DocumentJoiner-Result_1739380168023",
                    "intro": "DocumentJoiner-Result",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "join_mode": "concatenate",
                        "sort_by_score": true,
                        "top_k": null,
                        "weights": null
                    }
                },
                {
                    "name": "DocumentSplitter",
                    "type": "haystack.components.preprocessors.document_splitter.DocumentSplitter",
                    "component_id": "DocumentSplitter_1739380168023",
                    "intro": "DocumentSplitter",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "split_by": "word",
                        "split_length": 200,
                        "split_overlap": 200,
                        "split_threshold": 0
                    }
                },
                {
                    "name": "DocumentWriter",
                    "type": "haystack.components.writers.document_writer.DocumentWriter",
                    "component_id": "DocumentWriter_1739380168023",
                    "intro": "DocumentWriter",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "document_store": {
                            "init_parameters": {
                                "connection_string": {
                                    "env_vars": [
                                        "DATABASE_SYNC_URI"
                                    ],
                                    "strict": true,
                                    "type": "env_var"
                                },
                                "embedding_dimension": 1024,
                                "keyword_index_name": "haystack_keyword_index",
                                "recreate_table": true,
                                "table_name": "embedding_results",
                                "vector_function": "cosine_similarity"
                            },
                            "type": "byoa.integrations.document_stores.mo_document_store.MOIDocumentStore"
                        },
                        "policy": "NONE"
                    }
                },
                {
                    "name": "FileRouterComponent",
                    "type": "haystack.components.routers.file_type_router.FileTypeRouter",
                    "component_id": "FileRouterComponent_1739380168023",
                    "intro": "FileRouterComponent",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "additional_mimetypes": null,
                        "mime_types": [
                            "text/plain",
                            "text/markdown",
                            "image/.*",
                            "application/pdf"
                        ]
                    }
                },
                {
                    "name": "ImageCaptionToDocument",
                    "type": "byoa.integrations.components.converters.image_caption_to_document.ImageCaptionToDocument",
                    "component_id": "ImageCaptionToDocument_1739380168023",
                    "intro": "ImageCaptionToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {}
                },
                {
                    "name": "ImageOCRToDocument",
                    "type": "byoa.integrations.components.converters.image_ocr_to_document.ImageOCRToDocument",
                    "component_id": "ImageOCRToDocument_1739380168023",
                    "intro": "ImageOCRToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "model": "ucaslcl/GOT-OCR2_0",
                        "tokenizer": "stepfun-ai/GOT-OCR2_0"
                    }
                },
                {
                    "name": "ImageToDocument",
                    "type": "byoa.integrations.components.converters.image_to_document.ImageToDocument",
                    "component_id": "ImageToDocument_1739380168023",
                    "intro": "ImageToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {}
                },
                {
                    "name": "MagicPDFToDocument",
                    "type": "byoa.integrations.components.converters.magic_pdf_to_document.MagicPDFToDocument",
                    "component_id": "MagicPDFToDocument_1739380168023",
                    "intro": "MagicPDFToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {}
                },
                {
                    "name": "MarkdownToDocument",
                    "type": "haystack.components.converters.markdown.MarkdownToDocument",
                    "component_id": "MarkdownToDocument_1739380168023",
                    "intro": "MarkdownToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "progress_bar": false,
                        "table_to_single_line": false
                    }
                },
                {
                    "name": "MetadataRouter",
                    "type": "haystack.components.routers.metadata_router.MetadataRouter",
                    "component_id": "MetadataRouter_1739380168023",
                    "intro": "MetadataRouter",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "rules": {
                            "image": {
                                "conditions": [
                                    {
                                        "field": "meta.content_type",
                                        "operator": "==",
                                        "value": "image"
                                    }
                                ],
                                "operator": "AND"
                            },
                            "text": {
                                "conditions": [
                                    {
                                        "field": "meta.content_type",
                                        "operator": "==",
                                        "value": "text"
                                    }
                                ],
                                "operator": "AND"
                            }
                        }
                    }
                },
                {
                    "name": "PythonExecutor",
                    "component_id": "PythonExecutor_1739380168023",
                    "intro": "PythonExecutor",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "python_code": ""
                    },
                    "type": "byoa.integrations.components.python_executor.PythonExecutor"
                },
                {
                    "name": "TextFileToDocument",
                    "type": "haystack.components.converters.txt.TextFileToDocument",
                    "component_id": "TextFileToDocument_1739380168023",
                    "intro": "TextFileToDocument",
                    "position": {
                        "x": 0,
                        "y": 0
                    },
                    "input_keys": {},
                    "output_keys": {},
                    "init_parameters": {
                        "encoding": "utf8"
                    }
                }
            ],
            "connections": [
                {
                    "receiver": "TextFileToDocument.sources",
                    "sender": "FileRouterComponent.text/plain"
                },
                {
                    "receiver": "MarkdownToDocument.sources",
                    "sender": "FileRouterComponent.text/markdown"
                },
                {
                    "receiver": "ImageToDocument.sources",
                    "sender": "FileRouterComponent.image/.*"
                },
                {
                    "receiver": "MagicPDFToDocument.sources",
                    "sender": "FileRouterComponent.application/pdf"
                },
                {
                    "receiver": "DocumentJoiner.documents",
                    "sender": "TextFileToDocument.documents"
                },
                {
                    "receiver": "DocumentJoiner.documents",
                    "sender": "MarkdownToDocument.documents"
                },
                {
                    "receiver": "DocumentJoiner.documents",
                    "sender": "MagicPDFToDocument.documents"
                },
                {
                    "receiver": "DocumentJoiner.documents",
                    "sender": "ImageToDocument.documents"
                },
                {
                    "receiver": "MetadataRouter.documents",
                    "sender": "DocumentJoiner.documents"
                },
                {
                    "receiver": "DocumentCleaner.documents",
                    "sender": "MetadataRouter.text"
                },
                {
                    "receiver": "ImageOCRToDocument.documents",
                    "sender": "MetadataRouter.image"
                },
                {
                    "receiver": "ImageCaptionToDocument.documents",
                    "sender": "MetadataRouter.image"
                },
                {
                    "receiver": "DocumentSplitter.documents",
                    "sender": "DocumentCleaner.documents"
                },
                {
                    "receiver": "DocumentJoiner-Result.documents",
                    "sender": "DocumentSplitter.documents"
                },
                {
                    "receiver": "DocumentCleaner-ImageOCR.documents",
                    "sender": "ImageOCRToDocument.documents"
                },
                {
                    "receiver": "DocumentJoiner-Result.documents",
                    "sender": "DocumentCleaner-ImageOCR.documents"
                },
                {
                    "receiver": "DocumentCleaner-ImageCaption.documents",
                    "sender": "ImageCaptionToDocument.documents"
                },
                {
                    "receiver": "DocumentJoiner-Result.documents",
                    "sender": "DocumentCleaner-ImageCaption.documents"
                },
                {
                    "receiver": "PythonExecutor.documents",
                    "sender": "DocumentJoiner-Result.documents"
                },
                {
                    "receiver": "DocumentEmbedder.documents",
                    "sender": "PythonExecutor.documents"
                },
                {
                    "receiver": "DocumentWriter.documents",
                    "sender": "DocumentEmbedder.documents"
                }
            ],
            "edges": [],
            "extra_components": []
        }
    }
}
```

### 查看作业关联的文件列表

```
GET /byoa/api/v1/index_workflow_job/{job_id}/files
```

**输出参数：**
  
|  参数             | 含义 |
|  --------------- | ----  |
| id               |文件 id      |
| file_type        |文件类型，2 为 pdf。    |
|file_status       |文件状态 |

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow_job/0194f423-c2a7-7cc5-87ce-97fa942ac6ce/files"
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx",
    "Access-Token": "xxxx",
    "uid": "a6e11303-f4fd-46c0-b5ff-c774e96f64a3-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}
response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回

```bash
Response Body: {
    "code": "ok",
    "msg": "ok",
    "data": {
        "files": [
            {
                "id": "0194f423-c2a7-7ccc-a3da-732bafda96a3",
                "file_name": "红楼梦(通行本)简体横排.pdf",
                "file_type": 2,
                "file_status": 2,
                "error_message": "",
                "start_time": "2025-02-11T08:32:52.000000+0000",
                "end_time": "2025-02-11T08:37:53.000000+0000"
            }
        ],
        "total": 1,
        "completed": 1,
        "failed": 0,
        "processing": 0,
        "pending": 0
    }
}
```

### 重新处理失败文件

```
POST /byoa/api/v1/index_workflow_job/{job_id}/files
```

**输入参数：**
  
|  参数             | 是否必填 |含义|
|  --------------- | ----   | ----  |
| files            |是       | 文件 id|

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/byoa/api/v1/index_workflow_job/0194f423-c2a7-7cc5-87ce-97fa942ac6ce/files"

headers = {
    "user-id":"xxxx",
    "Access-Token": "xxxx",
    "uid": "011d4b66-ace5-4d58-88a4-bc76719acda5-0194dfaa-3eda-7ea5-b47c-b4f4f594xxxx:admin:accountadmin"
}

body = {
    "files": ["0194f423-c2a7-7ccc-a3da-732bafda96a3"]
}

response = requests.post(url, headers=headers)

if response.status_code == 200:
    print(response.json()) 
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

返回：

```bash
{'code': 'ok', 'msg': 'ok', 'data': None}
```