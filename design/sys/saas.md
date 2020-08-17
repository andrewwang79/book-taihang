# SAAS系统

# 系统
## 系统异同

| 系统 | 角色 | 推荐方案 | 说明 |
| :----: | ---- | ---- |
| 非SAAS系统(平台) | "平台角色" | 管理员表(无组织架构)，或者公司员工表 |  |
| SAAS系统(平台+商户) | "平台角色" + "商户角色" | 有2个子系统：平台管理系统(管理员表, 无组织架构)，商户管理系统(商户员工表) |  |

## 子系统构成

| 系统 | 使用人员 | 说明 |
| :----: | ---- | ---- |
| 平台管理 | "平台角色" | 可按照业务分离成多个内部管理系统 |
| 业务系统 | 用户 | 如用户APP之类的 |
| 商户业务管理 | "商户角色" |  |
| API | 无 |  |

# 角色
## 平台角色
### 基础

| 角色 | 编码 | 功能 | 说明 |
| :----: | ---- | ---- |
| 系统设计员 | GOD | 系统设计(页面) |  |
| 管理员 | ADMIN | 系统管理(菜单，角色，权限)，系统配置(如系统名称和图片等) |  |

### 业务

| 角色 | 编码 | 功能 | 说明 |
| :----: | ---- | ---- |
| 运营角色X | 业务自定义 | 业务自定义 | 一般有2个基础角色，运营(如业务管理和审核)和财务 |

## 商户角色
| 角色 | 编码 | 功能 | 说明 |
| :----: | ---- | ---- |
| 商户管理员 | 业务自定义(ADMIN) | 业务自定义 |  |
| 运营角色X | 业务自定义 | 业务自定义 | 基于商户业务 |

# 平台API列表

# 表结构
## 平台管理员(admin)
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 名字 | name | VARCHAR(100) | N |  |
| 头像 | head_image | VARCHAR(255) | Y |  |
| 电话 | mobile | VARCHAR(50) | N |  |
| 密码 | password | VARCHAR(100) | N |  |
| 角色 | role | VARCHAR(50) | N | 系统设计员(GOD)，管理员(ADMIN) |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  |  |

## 商户(merchant)
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 编码 | code | VARCHAR(255) | Y |  |
| 名称 | name | VARCHAR(500) | N |  |
| 电话 | mobile | VARCHAR(50) | Y |  |
| 地址 | address | VARCHAR(255) | Y |  |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  |  |

## 商户员工(merchant_employee)
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 商户id | merchant_id | LONG | N |  |
| 名字 | name | VARCHAR(100) | N |  |
| 头像 | head_image | VARCHAR(255) | Y |  |
| 电话 | mobile | VARCHAR(50) | N |  |
| 密码 | password | VARCHAR(100) | N |  |
| 角色 | role | VARCHAR(50) | N | 管理员(ADMIN)，总部财务，店长，店员等 |
| 状态 | status | VARCHAR(50) | Y |  正常，休假，离职等 |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  |  |
