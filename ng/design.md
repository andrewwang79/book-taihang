# 系统设计

## 整体结构
### 架构
| 层级 | package | 说明 |
| :----: | -- | -- |
| API层 | controller | 对外提供API服务。可以调用manager和service |
| 业务逻辑层 | manager | 可以调用service |
| 服务层 | service | 接入数据和外部服务 |

### 项目
```
API项目
  controller

middletier项目
  manager
  service
    UserService : 数据
    SmsService : 外部服务
  dao : mapper是MyBatis，repository是JPA
  entity
```

### 文件
#### controller
1. 函数命名规范 : CRUD
1. 函数顺序
  1. manager
  1. service

#### manager

#### service
1. 函数命名规范 : 同dao
1. 函数顺序: 同dao

#### dao
1. 函数命名规范 : JPA命名
1. 函数顺序
  1. 自定义
  1. query
  1. CRUD

#### 对象

## 注册方式
| 字段 | 对应 | 说明 |
| :-: | - | - |
| DO/PO/entity | 单表 |  |
| VO | 多表视图 | 多表查询 |
| DTO | 数据传输对象 | 如API的输入输出，有输入输出两个对象 |
| BO | 业务对象 | 内部使用。有时候直接作为输出DTO |
