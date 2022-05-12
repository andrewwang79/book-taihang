# 接口

## 租户信息

### 查询所有租户(/v1/tenant/search)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 页数 | page | Integer | Y | 从0开始 |
| 页容量 | pageSize | Integer | Y | 最小是1 |

```
{
	"page" : 0,
	"pageSize" : 5
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 总页数 | totalPages | Integer | Y |  |
| 总条数 | totalElements | Integer | Y |  |
| 结果集合 | list | List | Y |  |
| -- 租户Id | id | Integer | Y |  |
| -- 租户Code | code | String | Y |  |
| -- 租户名称 | name | String | Y |  |
| -- 租户状态 | status | Integer | Y | 1为启用  2为禁用 |

```  
{
    "code": 0,
    "data": {
        "list": [
            {
                "id": 1,
                "code": "TestTenantCode",
                "name": "TestName",
                "status": 1
            },
            {
                "id": 3,
                "code": "ZS",
                "name": "中山医院",
                "status": 2
            }
        ],
        "totalPages": 1,
        "totalElements": 5
    }
}
```

### 查询租户详情(/v1/tenant/read)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Id | id | Integer | Y |  |

```
{
    "id": 1
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户id | id | Integer | Y |  |
| 租户Code | code | String | Y |  |
| 租户名称 | name | String | Y |  |
| 租户电话 | mobile | String | Y |  |
| 租户地址 | address | String | Y |  |
| 备注 | remark | Text | N |  |

```
{
  "code": 0,
  "data": {
    "id": 1,
    "code": "TestCode",
    "name": "TestName",
    "mobile": "TestMobile",
    "address": "TestAddress",
    "remark": ""
  }
}
```

### 添加租户(/v1/tenant/create)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Code | code | String | Y |  |
| 租户名称 | name | String | Y |  |
| 租户电话 | mobile | String | Y |  |
| 租户地址 | address | String | Y |  |
| 备注 | remark | Text | N |  |

```
{
	"name" : "禅城医院",
	"code" : "CY",
	"mobile" : "18668987852",
	"address" : "上海",
	"remark" : ""
}
```

* 输出
```
{
  "code": 0 --成功
  "code": 401 --租户code已存在
}
```


### 禁用/启用租户(/v1/tenant/status/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Id | id | Integer | Y | |
| 租户状态 | status | Integer | Y | 1为 启用 2为禁用 |

```
{
	"id" : 5,
	"status" : 2
}
```

* 输出 ：无

### 编辑租户(/v1/tenant/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户id | id | Integer | Y | 不可修改 |
| 租户Code | code | String | Y |不可修改 |
| 租户名称 | name | String | Y |  |
| 租户电话 | mobile | String | Y |  |
| 租户地址 | address | String | Y |  |
| 备注 | remark | Text | N |  |


```
{
  "id": 2,
  "name": "禅医",
  "code": "CY",
  "mobile": "18668987852",
  "address": "上海",
  "remark": ""
}
```

* 输出 ：无

## 系统
### 根据租户Id查询所有系统(/v1/sys/search)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Id | tenantId | Integer | Y |  |
| 页数 | page | Integer | Y | 最小值0 |
| 页容量 | pageSize | Integer | Y | 最小值1 |


```
{
	"tenantId" : 1,
	"page" : 0,
	"pageSize" : 3
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 总页数 | totalPages | Integer | Y |  |
| 总条数 | totalElements | Integer | Y |  |
| 结果集合 | list | List | Y |  |
| -- 系统id | id | Integer | Y |  |
| -- 系统名称 | name | String | Y |  |
| -- 系统类型 | type | String | Y |  |
| -- 系统状态 | status | Integer | Y | 1为 启用 2为禁用 |

```
{
    "code": 0,
    "data": {
        "list": [
            {
                "id": 1,
                "name": "测试系统2",
                "type": "HIS",
                "status": 1
            },
            {
                "id": 2,
                "name": "测试系统2",
                "type": "HIS",
                "status": 2
            }
        ],
        "totalPages": 1,
        "totalElements": 3
    }
}
```

### 查询系统详情(/v1/sys/read)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | id | Integer | Y |  |

```
{
    "id": 1
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统id | id | Integer | Y |  |
| 系统名称 | name | String | Y |  |
| 系统类型 | type | String | Y |  |
| 系统状态 | status | String | Y |  |
| 租户id | tenantId | Integer | Y |  |

```
{
    "code": 0,
    "data": {
        "id": 2,
        "name": "测试系统2",
        "type": "HIS",
        "status": 2,
        "tenantId": 1
    }
}
```

### 添加系统(/v1/sys/create)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统名称 | name | String | Y |  |
| 系统类型 | type | String | Y |  |
| 租户id | tenantId | Integer | Y |  |


```
{
	"name": "sys1",
	"type": "PACS",
	"tenantId" : 1
}
```

* 输出 ：无

### 禁用/启用系统(/v1/sys/status/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Id | id | Integer | Y | |
| 租户状态 | status | Integer | Y | 1为 启用 2为禁用 |

```
{
	"id" : 1,
	"status" : 2
}
```

* 输出 ：无

### 编辑系统(/v1/sys/edit)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统id | id | Integer | Y | 不可修改 |
| 系统名称 | name | String | Y |  |
| 系统类型 | type | String | Y |  |
| 租户id | tenantId | Integer | Y | 不可修改 |

```
{
	"id": 1,
	"name" : "测试系统1",
	"type" : "Pacs",
	"tenantId" : 1
}
```

* 输出 ：无

## 配置信息
### 查询系统下的配置(/v1/sys/dict/query)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | sysId | Integer | Y |  |

```
{
	"sysId" : 1
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回集合 | list | List | Y |  |
| -- 系统id | sysId | Integer | Y |  |
| -- 实例 | name | String | Y |  |
| -- 类型 | type | String | Y |  |
| -- 实例描述 | nameDescription | String | Y |  |
| -- 类型描述 | typeDescription | String | Y |  |

```
{
    "code": 0,
    "data": {
        "list": [
            {
                "name": "db",
                "type": "dataType",
                "sysId": "1",
                "nameDescription": "DB集成配置",
                "typeDescription": "检查信息获取配置"
            }
        ]
    }
}
```

### 删除系统配置信息(/v1/sys/dict/delete)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | sysId | String | Y |  |
| 类型 | type | String | Y |  |

```
{
	"type":"dataType",
	"sysId":"1"
}
```

* 输出：无


### 添加配置信息(/v1/sys/dict/create)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 配置集合 | createDtoInfoList | List | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | N |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
| -- 系统Id | sysId | String | Y |  |

```
{
  "createDtoInfoList": [
    {
      "parentKey": "dbConnect",
      "dictKey": "dbType",
      "dictValue": "sqlserver",
      "dictType": "dataType",
      "sysId": "1",
      "description": "数据库类型"
    },
    {
      "parentKey": "dbConnect",
      "dictKey": "dbUrl",
      "dictValue": "sqlserver",
      "dictType": "dataType",
      "sysId": "1",
      "description": "数据库链接地址"
    },
    {
      "parentKey": "dbConnect",
      "dictKey": "userName",
      "dictValue": "sa",
      "dictType": "dataType",
      "sysId": "1",
      "description": "用户名"
    },
    {
      "parentKey": "dbConnent",
      "dictKey": "password",
      "dictValue": "crz",
      "dictType": "dataType",
      "sysId": "1",
      "description": "密码"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientId",
      "dictValue": "sick_id",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者编号"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientName",
      "dictValue": "sick_name",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者姓名"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientNameEng",
      "dictValue": "sick_name_py",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者姓名(英文)"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientSex",
      "dictValue": "sick_sex",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者性别"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientAge",
      "dictValue": "sick_age",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者年龄"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "patientBirthdate",
      "dictValue": "sick_birthdate",
      "dictType": "dataType",
      "sysId": "1",
      "description": "患者生日"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "studyId",
      "dictValue": "study_id",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查编号"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "studyInstanceUid",
      "dictValue": "StudyUID",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查唯一编号"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "studyStatus",
      "dictValue": null,
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查状态"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "studyCharacteristics",
      "dictValue": null,
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查方法"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "studyDatetime",
      "dictValue": "study_date",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查时间"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "bodyPart",
      "dictValue": "study_part",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查部位"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "modality",
      "dictValue": "device_type",
      "dictType": "dataType",
      "sysId": "1",
      "description": "设备类型"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "reportDatetime",
      "dictValue": "report_date",
      "dictType": "dataType",
      "sysId": "1",
      "description": "报告时间"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "reportFinding",
      "dictValue": "jc_see",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查所见"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "reportDiagnose",
      "dictValue": "jc_diag",
      "dictType": "dataType",
      "sysId": "1",
      "description": "检查总结"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "positive",
      "dictValue": null,
      "dictType": "dataType",
      "sysId": "1",
      "description": "阴阳性"
    },
    {
      "parentKey": "tableColumn",
      "dictKey": "url",
      "dictValue": null,
      "dictType": "dataType",
      "sysId": "1",
      "description": "dcm地址"
    }
  ]
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | data | boolean | Y | true 修改成功 false 失败 |

```
{
    "code": 0,
    "data": true
}
```

### 添加配置信息(/v1/sys/dict/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 配置集合 | createDtoInfoList | List | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | N |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
| -- 系统Id | sysId | String | Y |  |

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | data | boolean | Y | true 修改成功 false 失败 |

```
{
    "code": 0,
    "data": true
}
```

### 查询检查信息获取配置的子配置详情的标题头(/v1/sys/dict/data/bar/query)
* 输入:无

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | dataList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
    "code": 0,
    "data": {
        "dataList": [
            {
                "id": 2,
                "parentKey": "dataType",
                "dictKey": "db",
                "dictValue": null,
                "dictType": "dataType",
                "description": "DB集成配置"
            },
            {
                "id": 3,
                "parentKey": "dataType",
                "dictKey": "webservice",
                "dictValue": null,
                "dictType": "dataType",
                "description": "Webservice"
            },
            {
                "id": 4,
                "parentKey": "dataType",
                "dictKey": "null",
                "dictValue": null,
                "dictType": "dataType",
                "description": "无"
            }
        ]
    }
}
```

### 查询检查信息获取配置的子配置详情(/v1/sys/dict/data/value/query)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | sysId | String | N |  |
| 影像获取类型 | dictKey | String | Y | dcmPull/webservice/currency |

* 输出
1. dictKey为dcmPull

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | dbList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
| 返回值 | tableColumnList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
    "code": 0,
    "data": {
        "dcmTypeInfoList": [
            {
                "id": 73,
                "parentKey": "dcmPull",
                "dictKey": "connection",
                "dictValue": "",
                "dictType": "dcmType",
                "sysId": null,
                "description": "连接信息"
            },
            {
                "id": 77,
                "parentKey": "dcmPull",
                "dictKey": "level",
                "dictValue": "seriesLevel",
                "dictType": "dcmType",
                "sysId": null,
                "description": "Move级别"
            }
        ],
        "connectionInfoList": [
            {
                "id": 74,
                "parentKey": "connection",
                "dictKey": "dcmHost",
                "dictValue": null,
                "dictType": "dcmPull",
                "sysId": null,
                "description": "PACS Ip"
            },
            {
                "id": 75,
                "parentKey": "connection",
                "dictKey": "dcmPort",
                "dictValue": null,
                "dictType": "dcmPull",
                "sysId": null,
                "description": "PACS 端口"
            },
            {
                "id": 76,
                "parentKey": "connection",
                "dictKey": "dcmAet",
                "dictValue": null,
                "dictType": "dcmPull",
                "sysId": null,
                "description": "PACS AETitle"
            }
        ],
        "levelInfoList": [
            {
                "id": 78,
                "parentKey": "level",
                "dictKey": "studyLevel",
                "dictValue": null,
                "dictType": "dcmPull",
                "sysId": null,
                "description": "Study级别"
            },
            {
                "id": 79,
                "parentKey": "level",
                "dictKey": "seriesLevel",
                "dictValue": "",
                "dictType": "dcmPull",
                "sysId": null,
                "description": "Series级别"
            }
        ],
        "levelParamInfoList": [
            {
                "id": 82,
                "parentKey": "studyLevel",
                "dictKey": "move",
                "dictValue": "StudyInstanceUid",
                "dictType": "level",
                "sysId": null,
                "description": "StudyLevelMoveKey"
            },
            {
                "id": 80,
                "parentKey": "seriesLevel",
                "dictKey": "find",
                "dictValue": "StudyInstanceUid",
                "dictType": "level",
                "sysId": null,
                "description": "SeiesLevelFindKey"
            },
            {
                "id": 81,
                "parentKey": "seriesLevel",
                "dictKey": "move",
                "dictValue": "SeriesInstanceUid",
                "dictType": "level",
                "sysId": null,
                "description": "SeriesLevelMoveKey"
            }
        ]
    }
}
```

1. dictKey为webservice/currency

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | dataList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
    "code": 0,
    "data": {
        "dataTypeInfoList": [
            {
                "id": 64,
                "parentKey": "webservice",
                "dictKey": "client",
                "dictValue": null,
                "dictType": "dataType",
                "sysId": null,
                "description": "请求型Webservice"
            },
            {
                "id": 65,
                "parentKey": "webservice",
                "dictKey": "server",
                "dictValue": null,
                "dictType": "dataType",
                "sysId": null,
                "description": "接收型Webservice"
            }
        ]
    }
}
```

### 查询影像信息获取配置的子配置详情的标题头(/v1/sys/dict/dcm/bar/query)
* 输入:无

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | dataList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
```
{
    "code": 0,
    "data": {
        "dataList": [
            {
                "id": 65,
                "parentKey": "dcmType",
                "dictKey": "dcmPull",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "DICOM Q/R"
            },
            {
                "id": 66,
                "parentKey": "dcmType",
                "dictKey": "dcmPush",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "DICOM SCP"
            },
            {
                "id": 67,
                "parentKey": "dcmType",
                "dictKey": "webservice",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "Webservice"
            },
            {
                "id": 68,
                "parentKey": "dcmType",
                "dictKey": "ftpUpload",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "FTP UPLOAD"
            },
            {
                "id": 69,
                "parentKey": "dcmType",
                "dictKey": "ftpDown",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "FTP DOWN"
            },
            {
                "id": 70,
                "parentKey": "dcmType",
                "dictKey": "fsCopy",
                "dictValue": null,
                "dictType": "dcmType",
                "description": "445共享文件夹"
            }
        ]
    }
}
```

### 查询影像信息获取配置下的子配置详情(/v1/sys/dict/dcm/value/query)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | sysId | String | N |  |
| 影像获取类型 | dictKey | String | Y |  |

```
{
	"dictKey":"dcmPull"
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| DCM相关配置 | dcmTypeInfoList | list | Y |  |
| DCM连接配置 | connectionInfoList | list | Y |  |
| DCM move级别配置| levelInfoList | list | Y |  |
| Find /move级别入参配置 | levelParamInfoList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
  "code": 0,
  "data": {
    "dcmTypeInfoList": [
      {
        "id": 117,
        "parentKey": "dcmPull",
        "dictKey": "level",
        "dictValue": "seriesLevel",
        "dictType": "dcmType",
        "sysId": null,
        "description": "Move级别"
      },
      {
        "id": 199,
        "parentKey": "dcmPull",
        "dictKey": "connection",
        "dictValue": "",
        "dictType": "dcmType",
        "sysId": null,
        "description": "连接信息"
      }
    ],
    "connectionInfoList": [
      {
        "id": 83,
        "parentKey": "connection",
        "dictKey": "dcmHost",
        "dictValue": null,
        "dictType": "dcmPull",
        "sysId": null,
        "description": "PACS Ip"
      },
      {
        "id": 84,
        "parentKey": "connection",
        "dictKey": "dcmPort",
        "dictValue": null,
        "dictType": "dcmPull",
        "sysId": null,
        "description": "PACS 端口"
      },
      {
        "id": 85,
        "parentKey": "connection",
        "dictKey": "dcmAet",
        "dictValue": null,
        "dictType": "dcmPull",
        "sysId": null,
        "description": "PACS AETitle"
      }
    ],
    "levelInfoList": [
      {
        "id": 118,
        "parentKey": "level",
        "dictKey": "studyLevel",
        "dictValue": null,
        "dictType": "dcmPull",
        "sysId": null,
        "description": "Study级别"
      },
      {
        "id": 119,
        "parentKey": "level",
        "dictKey": "seriesLevel",
        "dictValue": "",
        "dictType": "dcmPull",
        "sysId": null,
        "description": "Series级别"
      }
    ],
    "levelParamInfoList": [
      {
        "id": 121,
        "parentKey": "studyLevel",
        "dictKey": "move",
        "dictValue": null,
        "dictType": "level",
        "sysId": null,
        "description": "StudyLevelMoveKey"
      },
      {
        "id": 120,
        "parentKey": "seriesLevel",
        "dictKey": "find",
        "dictValue": "StudyInstanceUid",
        "dictType": "level",
        "sysId": null,
        "description": "SeiesLevelFindKey"
      }
    ]
  }
}
```

### 查询数据库字段值配置的所有类型(/v1/sys/dict/column/bar/query)
* 输入:无

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | dataList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
  "code": 0,
  "data": {
    "dataList": [
      {
        "id": 240,
        "parentKey": "columnValue",
        "dictKey": "tableColumnValue",
        "dictValue": null,
        "dictType": "columnValue",
        "description": "数据库字段值配置"
      }
    ]
  }
}
```

### 查询数据库字段值配置获取配置详情(/v1/sys/dict/column/value/query)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统Id | sysId | String | N |  |
| 影像获取类型 | dictKey | String | Y | |

```
{
	"dictKey":"tableColumnValue"
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 数据库字段值配置集合 | tableColumnValueList | List | Y |  |
| 设备类型配置集合 | modalityList | List | Y |  |
| 检查部位配置集合 | bodyPartList | List | Y |  |
| 检测方法配置集合 | studyCharacteristicsList | List | Y |  |
| 患者性别配置集合 | patientSexList | List | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
| -- 系统Id | sysId | String | Y |  |

```
{
  "code": 0,
  "data": {
    "tableColumnValueList": [
      {
        "id": 269,
        "parentKey": "tableColumnValue",
        "dictKey": "modality",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "设备类型"
      },
      {
        "id": 270,
        "parentKey": "tableColumnValue",
        "dictKey": "bodyPart",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "检查部位"
      }
    ],
    "modalityList": [
      {
        "id": 273,
        "parentKey": "modality",
        "dictKey": "DR",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "DR"
      },
      {
        "id": 274,
        "parentKey": "modality",
        "dictKey": "CT",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "CT"
      },
      {
        "id": 293,
        "parentKey": "bodyPart",
        "dictKey": "OT",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "其他"
      }
    ],
    "studyCharacteristicsList": [
      {
        "id": 304,
        "parentKey": "studyCharacteristics",
        "dictKey": "CTE",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "CTE"
      }
    ],
    "patientSexList": [
      {
        "id": 294,
        "parentKey": "patientSex",
        "dictKey": "M",
        "dictValue": null,
        "dictType": "tableColumnValue",
        "sysId": null,
        "description": "男"
      }
    ]
  }
}
```

### 查询设备AE的子配置的标题头(/v1/sys/dict/device/bar/query)
* 输入:无

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | deviceList | list | Y |  |
| -- 配置id | id | Integer | Y |  |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | Y |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 系统Id | sysId | String | Y |  |
| -- 备注 | description | String | Y |  |

```
{
  "code": 0,
  "data": {
    "deviceList": [
      {
        "id": 1808,
        "parentKey": "deviceType",
        "dictKey": "device",
        "dictValue": null,
        "dictType": "deviceType",
        "sysId": null,
        "description": "设备信息配置"
      }
    ]
  }
}
```

### 测试数据库连接信息(/v1/sys/dict/db/connection/check)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 数据库类型 | dbType | String | Y |  |
| 数据库链接地址 | dbUrl | String | Y |  |
| 用户名 | userName | String | Y | |
| 密码 | password | String | Y | |

```
{
	"dbType":"sqlserver",
	"dbUrl":"jdbc:sqlserver://172.16.100.104:1433;DatabaseName=pacs",
	"userName":"sa",
	"password":"crz"
}
```
* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | data | boolean | Y | true 连接成功 false 失败 |

```
{
    "code": 0,
    "data": true
}
```

### 测试DCM连接信息(/v1/sys/dict/dcm/connection/check)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| AET | dcmAet | String | Y |  |
| IP | dcmHost | String | Y |  |
| 端口 | dcmPort | String | Y | |

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 返回值 | data | boolean | Y | true 成功 false 失败 |

```
{
    "code": 0,
    "data": true
}
```

##系统设备AET配置
###查看当前系统的设备AE配置详情(/v1/sys/dicom/device/search)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 页数 | page | INTEGER | Y |  |
| 条数 | pageSize | INTEGER | Y |  |
| 系统id | sysId | INTEGER | Y | |

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 总页数 | totalPages | INTEGER | Y |  |
| 总条数 | totalElements | INTEGER | Y |  |
| 设备AE list | list | LIST | Y | |
| --自增id | id | INTEGER | Y | |
| --系统id | sysId | INTEGER | Y | |
| --设备ae | aeTitle | String | Y | |
| --设备ae描述 | description | String | Y | |

```
{
  "code": 0,
  "data": {
    "list": [
      {
        "id": 3,
        "sysId": 1,
        "aeTitle": "TEST",
        "description": "CESI"
      }
    ],
    "totalPages": 1,
    "totalElements": 1
  }
}
```

### 查看当前系统的某个设备AE详情(/v1/sys/dicom/device/read)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 设备AE配置自增id | id | INTEGER | Y |  |

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 设备AE配置自增id | id | INTEGER | Y |  |
| 系统id | sysId | INTEGER | Y | |
| 设备ae | aeTitle | STRING | Y | |
| 设备ae描述 | description | STRING | N | |

```
{
  "code": 0,
  "data": {
    "id": 6,
    "sysId": 1,
    "aeTitle": "TEST",
    "description": "CESI"
  }
}
```

### 删除当前系统的设备AE配置详情(/v1/sys/dicom/device/delete)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 设备AE配置自增id | id | INTEGER | Y |  |

* 输出:无

### 新增当前系统的设备AE配置详情(/v1/sys/dicom/device/create)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 系统id | sysId | INTEGER | Y | |
| 设备ae | aeTitle | String | Y | |
| 设备ae描述 | description | String | N | |
| DICOM设备AE配置字典表头配置 | deviceInfoList | List | L | |
| -- 配置key | dictKey | String | Y |  |
| -- 父节点 key | parentKey | String | Y |  |
| -- 配置value | dictValue | String | N |  |
| -- 配置类型 | dictType | String | Y |  |
| -- 备注 | description | String | Y |  |
| -- 系统Id | sysId | String | Y |  |

```
{
  "sysId": 1,
  "aeTitle": "TEST",
  "description": "CESI",
  "deviceInfoList": [
    {
      "sysId": "1",
      "parentKey": "sys",
      "dictKey": "deviceType",
      "dictValue": "device",
      "dictType": "deviceType",
      "description": "设备信息配置"
    }
  ]
}
```

* 输出

```
{
    "code": 401,
    "msg": "数据已存在"
}
```

### 修改当前系统的设备AE配置详情(/v1/sys/dicom/device/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 自增id | id | INTEGER | Y | |
| 系统id | sysId | INTEGER | Y | |
| 设备ae | aeTitle | STRING | Y | |
| 设备ae描述 | description | STRING | N | |

* 输出:无

## broker 对接上层产品

## filter
### 添加上层产品获取数据条件(/v1/filter/create)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 队列名称 | queueName | String | Y | |
| 租户Code | tenantCode | String | Y | |
| 条件 | filter | String | Y | |
| --设备类型 | modality | String | 	Y | |
| --检查部位 | bodyPart | String | N | |
| --检查描述 | studyDescription | String | N | |
| --序列描述 | seriesDescription | String | N | |
| --扫描序列名 | protocolName | String | N | |

```
{
  "queueName": "ring_queue",
  "tenantCode": "0000",
  "filter": {
    "modality": "CT,DR",
    "bodyPart": "CHEST,PELVIS",
    "studyDescription": "chest,thorax,lung,thorroutine,胸,肺,肋",
    "seriesDescription": "chest,thorax,lung,thorroutine,胸,肺,肋",
    "protocolName": "chest,thorax,lung,thorroutine,胸,肺,肋"
  }
}
```

* 输出：无

### 根据队列名称、租户Code 查询产品获取检查信息(/v1/filter/get_by_queueName_tenantCode)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 队列名称 | queueName | String | Y | |
| 租户Code | tenantCode | String | Y | |

```
{
	"queueName": "ring_queue",
  "tenantCode":"0000"
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| id | id | Integer | Y | |
| 队列名称 | queueName | String | Y | |
| 租户Code | tenantCode | String | Y | |
| 设备类型 | modality | String | 	Y | |
| 检查部位 | bodyPart | String | Y |
| 检查描述 | studyDescription | String | Y | |
| 序列描述 | seriesDescription | String | Y | |
| 扫描序列名 | protocolName | String | Y |

```
{
  "code": 0,
  "data": {
    "id": 2,
    "queueName": "ring_queue",
    "tenantCode": "0000",
    "modality": "CT,DR",
    "bodyPart": "CHEST,PELVIS",
    "studyDescription": "chest,thorax,lung,thorroutine,胸,肺,肋",
    "seriesDescription": "chest,thorax,lung,thorroutine,胸,肺,肋",
    "protocolName": "chest,thorax,lung,thorroutine,胸,肺,肋"
  }
}
```

### 修改上层产品获取数据条件(/v1/filter/update)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| id | id | Integer | Y | |
| 队列名称 | queueName | String | N | |
| 租户Code | tenantCode | String | N | |
| 条件 | filter | String | N | |
| --设备类型 | modality | String | N | |
| --检查部位 | bodyPart | String | N | |
| --检查描述 | studyDescription | String | N | |
| --序列描述 | seriesDescription | String | N | |
| --扫描序列名 | protocolName | String | N | |

```
{
  "id": 2,
  "queueName": "ring_queue",
  "tenantCode": "0000",
  "filter": {
	"modality": "CT,DR,MR"
  }
}
```
* 输出: 无

## 上传ZIP/.dcm文件
### 根据队列名称、租户Code 查询产品获取检查信息(/v1/file//upload)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Code | tenantCode | String | Y | |
| 操作人 | userName | String | Y | |
| 文件 | file | MultipartFile[] | N |

* 输出:无

* code码

```
80 参数错误
1/902  统一都是上传失败
903/904/900  统一都是解析失败
905 dcm文件校验失败
902 文件为空
```

### 查询上传记录(/v1/file/search)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 租户Code | tenantCode | String | Y |  |
| 页数 | page | Integer | Y | 从0开始 |
| 页容量 | pageSize | Integer | Y | 最小是1 |

```
{
	"page":0,
	"pageSize":10,
	"tenantCode":"1010"
}
```

* 输出

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| 总页数 | totalPages | Integer | Y |  |
| 总条数 | totalElements | Integer | Y |  |
| 结果集合 | list | List | Y |  |
| -- Id | id | Integer | Y |  |
| -- 操作人 | userName | String | Y |  |
| -- 检查号 | accessionNumber | String | N  |
| -- 检查UID | studyInstanceUid | String | N  |
| -- 文件名称 | fileName | String | N | |
| -- 文件大小 | fileLength | Long | N | 单位B |
| -- 上传时间 | createTime | Date | Y | |

```
{
  "code": 0,
  "data": {
    "list": [
      {
        "id": 43,
        "userName": "Admin",
				"accessionNumber":null,
        "studyInstanceUid": "0003393354",
        "fileName": "000001.zip",
        "fileLength": 237299700,
        "createTime": "2019-05-10 00:12:06"
      }
    ],
    "totalPages": 5,
    "totalElements": 41
  }
}
```

### 删除上传记录(/v1/file/delete)
* 输入

| 名称 | 字段 | 类型 | 必须 | 说明 |
| :-: | - | - | - | - |
| ID | id | Integer | Y |  |

```
{
	"id":11
}
```

* 输出：无
