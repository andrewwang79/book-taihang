# 通用结构

## 表字段
### 表结构

| 字段 | 名称 | 类型 | 必须 | 说明 |
| :----: | ---- | ---- | ---- |
| is_delete | 逻辑删除 | BOOL | Y | 有小部分表不需要逻辑删除功能 |
| createtime | 创建时间 | DATE  | Y |  |
| disable | 禁用 | BOOL  | N | 禁用功能 |
| audit_status | 审核状态 | BYTE  | N | 审核功能 |

### 定义
| 字段 | 名称 | 类型 |
| :----: | ---- | ---- |
| 编码 | code | VARCHAR(50) |
| 姓名/名称 | name | VARCHAR(50) |
| 手机 | mobile | VARCHAR(50) |
| 短说明 | remark | VARCHAR(1000) |
| 网址 | url | VARCHAR(1024) |

## 基础
### 分类(th_taxonomy)
复用字典表

| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y |  |
| 上级 | parent_id | LONG | N | NULL是根节点 |
| 名称 | name | VARCHAR(50) | Y |  |
| 分组 | group | VARCHAR(50) | Y | 逻辑分割组，如菜单是个组 |
| 数据 | data | VARCHAR(1000) | N | 自定义使用，比如菜单的url |
| 显示顺序 | seq | INT | Y | 大的显示在前面，默认是0 |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

## 常用
### 单据状态调整历史(th_order_status_change_hs)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 单据类型 | order_type | VARCHAR(100) | N |  |
| 单号 | order_id | Long | N |  |
| 单据状态 | order_status | VARCHAR(50) | N |  |
| 创建时间 | createtime | DATE | N |  |

## SAAS多租户
### 平台管理员(th_admin)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 账号 | account | VARCHAR(50) | Y |  |
| 名字 | name | VARCHAR(50) | Y |  |
| 头像 | head_image | VARCHAR(1024) | N |  |
| 手机 | mobile | VARCHAR(50) | Y |  |
| 密码 | password | VARCHAR(100) | Y | MD5密码 |
| 角色 | role | VARCHAR(50) | Y | 管理员(ADMIN)，设计待定 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 租户(th_tenant)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y |  |
| 名称 | name | VARCHAR(50) | Y |  |
| 手机 | mobile | VARCHAR(50) | N |  |
| 地址 | address | VARCHAR(255) | N |  |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |
