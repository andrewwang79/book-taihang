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

#### entity
1. 完整对应表结构
