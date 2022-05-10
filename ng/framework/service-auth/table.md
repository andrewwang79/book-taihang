# 表结构
## 权限
### 用户/员工(user)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 账号 | account | VARCHAR(50) | Y | 相当于工号 |
| 姓名 | name | VARCHAR(50) | Y |  |
| 头像 | head_image | VARCHAR(1024) | N |  |
| 手机 | mobile | VARCHAR(50) | N |  |
| 密码 | password | VARCHAR(50) | Y | 密码=MD5(pwd+salt) |
| SALT | salt | VARCHAR(10) | Y | 随机预生成 |
| 状态 | status | BYTE | Y |  正常，休假，离职等 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 角色(role)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y | FINANCE |
| 名称 |name| VARCHAR(50) | Y |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 权限(authority)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y | USER:CREATE |
| 名称 |name| VARCHAR(50) | Y |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 用户_角色(user_role)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 用户 | user_id | LONG | Y |  |
| 角色 | role_id | LONG | Y |  |

### 角色_权限(role_authority)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 角色 | role_id | LONG | Y |  |
| 权限 | authority_id | LONG | Y |  |

### 菜单(menu)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 上级 | parent_id | LONG | N | NULL是根节点 |
| 名称 |name| VARCHAR(50) | Y |  |
| 图标 | icon | VARCHAR(1024) | N | 图标css的class |
| 网址 | url | VARCHAR(1024) | Y |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 权限可用的菜单(authority_menu)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 权限 | authority_id | LONG | Y |  |
| 菜单 | menu_id | LONG | Y |  |

## 组织架构和组

### 组织架构(org)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y |  |
| 上级 | parent_id | LONG | N | NULL是根节点 |
| 名称 | name | VARCHAR(50) | Y | 信息科 |
| 手机 | mobile | VARCHAR(50) | N |  |
| 显示顺序 | seq | INT | Y | 大的显示在前面，默认是0 |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 组织架构_员工(org_user)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 部门 | org_id | LONG | Y |  |
| 职位 | position | VARCHAR(50) | Y |  |
| 员工 | user_id | LONG | Y |  |

### 组(group)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y |  |
| 名称 | name | VARCHAR(50) | Y | 信息科维护组 |
| 手机 | mobile | VARCHAR(50) | N |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

### 组员(group_user)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 组 | group_id | LONG | Y |  |
| 员工 | user_id | LONG | Y |  |
| 职位 | position | VARCHAR(50) | Y |  |

### 组织_角色(org_role)
* 组织和职位至少有1个
* TODO 方案待定。截止目前，在组织的人自动有权限，还没有好方案

| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 组织类型 | type | BYTE | Y | 组织架构，组 |
| 组织 | org_id | LONG | N |  |
| 职位 | position | VARCHAR(50) | N |  |
| 角色 | role_id | LONG | Y |  |
