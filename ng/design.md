# 系统设计

## 整体结构
### 架构
| 层级 | package | 说明 |
| :----: | -- | -- |
| 展示层 | / | 前端 |
| 接口层 | controller | 对外提供API服务。调用manager和service |
| 业务层 | manager | 业务逻辑，调用service |
| 服务层 | service | 数据逻辑和外部服务，调用数据层(UserService)和外部服务(SmsService) |
| 数据层 | dao | mapper是MyBatis，repository是JPA |

### 项目
```
frontend
server
  项目API
    controller
  项目middletier
    manager
    service
    dao
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
* 推荐方案：后端无VO，接口层用DTO；VO用于前端

| 名词 | 名称 | 对应层 | 对应对象 | 说明 |
| :-: | - | - | - | - |
| VO | 视图对象(View Object) | 展示层 | 页面/组件的数据封装 | 接口层数据的二次加工 |
| DTO | 数据传输对象(Data Transfer Object) | 所有层 | 层与层之间的数据传输 | 接口层有输入DTO和输出DTO |
| BO | 业务对象(Biz Object) | 业务层 | 业务层对象 | 内部使用。少部分情况下结构接口层DTO |
| ENTITY | 实体 | 数据层 | 数据库表 |  |
| PO | 持久化对象(Persistent Object) | 数据层 | 数据库表 |  |
| DM | 领域模型(Domain Model) | 数据层 | 数据库表 |  |
