# 用户权限

## 需求
1. 业务:菜单，页面功能/元素，API
1. 数据：数据显示(SELECT)，数据类型(WHERE)，组织架构层级(WHERE)

### 场景
#### 销售业务
1. 店长能看到店的月报，销售员看不到
1. 销售员看到用户信息（不含手机），店长看到用户信息（含手机）
1. 城市经理能看到城市的销售记录，省经理能看到整个省的销售记录

#### 内部管理
1. 部门经理能打印，员工不能打印
1. 本部门有数据A。部门经理DL1看数据A，员工DL2看数据A
1. 下级部门有数据B。部门经理DL2看数据B
1. 同级部门有数据C。部门经理需申请查看数据C

## 设计
### 概要
* 基于RBAC授权和基于用户授权的细粒度权限控制通用平台，并提供单点登录、会话管理和日志管理。
* 接入的系统可自由定义组织、角色、权限、资源等。用户权限=所拥有角色权限合集+用户加权限-用户减权限，优先级：用户减权限>用户加权限>角色权限

### 原则
1. 职位只是信息，和权限无关
1. 将所有业务定义成权限
1. 权限可以分配给角色，不能分配给人
1. 1个用户可有多个角色，暂不支持继承(权限/角色)
1. 角色可以分配给人或组
1. 组和组织架构是独立的两个概念
1. 权限可以分配到组织架构&职位，组&职位

### 权限
* 权限无类型
* 实例：订单查看，订单修改，订单打印，报告打印等

### 权限清单
1. 用户角色权限
1. 用户所在组织架构
1. 用户所在组织架构的职位
1. 用户所在组
1. 用户所在组的职位

用户权限可缓存，在其对应关系有调整时重新计算并缓存

### 数据权限设计
1. 不同业务功能是不同页面和权限。比如对于报告，有3个页面：查看部门报告(部门经理)，查看部门报告(普通职员)，查看本人报告
1. 报告安全等级是权限，不同的角色有不同的等级权限
1. 某个科室的数据查看是权限，通过组赋予本权限

### 菜单
1. 1个权限对应N个可启用的菜单
1. 1个菜单启用最多只需要1个权限

### 页面
1. 实现：业务权限和页面功能/元素的映射关系，页面预置。参考：
```
<shiro:hasRole name="admin">
  这是admin角色登录
</shiro:hasRole>
<shiro:hasPermission name="user:create">
  有user:create权限信息
</shiro:hasPermission>
```
1. 映射关系
  1. 功能：页面打印功能
  1. 按钮：页面修改按钮
  1. 块元素：页面高级TAB

### API
* 数据关联机制保障权限：不能查看其权限无关的信息
* 使用：@RequiresPermissions("RESOURCE:VIEW")
* 暂不开发

### 组的权限设计
1. 把权限授权给组，组中的用户/机构就自动拥有这些角色/权限
1. 实例
  1. 影像数据管理员(角色)的权限 = 组管理员 + 影像数据管理
  1. 行政数据管理(角色)的权限 = 组管理员 + 行政数据管理
  1. 组员1的角色 = 组员 + 影像数据查阅

### 组织架构
1. 结构：公司 -> 部门(允许多层) -> 员工
1. 部门只能属于1个公司
1. 1个员工只有1个职位
1. 1个员工可属于多个部门

### 操作分工
#### 运营人员
1. 用户管理，分配角色到用户
1. 角色管理，分配权限到角色
1. 权限和菜单配置
1. 组织架构管理

#### 超级管理员
1. 权限编辑

## 表结构
### 权限
#### 用户/员工(user)
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

#### 角色(role)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y | FINANCE |
| 名称 |name| VARCHAR(50) | Y |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

#### 权限(authority)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y | USER:CREATE |
| 名称 |name| VARCHAR(50) | Y |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

#### 用户_角色(user_role)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 用户 | user_id | LONG | Y |  |
| 角色 | role_id | LONG | Y |  |

#### 角色_权限(role_authority)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 角色 | role_id | LONG | Y |  |
| 权限 | authority_id | LONG | Y |  |

#### 菜单(menu)
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

#### 权限可用的菜单(authority_menu)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 权限 | authority_id | LONG | Y |  |
| 菜单 | menu_id | LONG | Y |  |

### 组织架构和组

#### 组织架构(org)
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

#### 组织架构_员工(org_user)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 部门 | org_id | LONG | Y |  |
| 职位 | position | VARCHAR(50) | Y |  |
| 员工 | user_id | LONG | Y |  |

#### 组(group)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 编码 | code | VARCHAR(50) | Y |  |
| 名称 | name | VARCHAR(50) | Y | 信息科维护组 |
| 手机 | mobile | VARCHAR(50) | N |  |
| 状态 | status | BYTE | Y | 启用/停用 |
| 说明 | remark | VARCHAR(1000) | N |  |
| 创建时间 | createtime | DATE | Y |  |

#### 组员(group_user)
| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 组 | group_id | LONG | Y |  |
| 员工 | user_id | LONG | Y |  |
| 职位 | position | VARCHAR(50) | Y |  |

#### 组织_角色(org_role)
* 组织和职位至少有1个
* TODO 方案待定。截止目前，在组织的人自动有权限，还没有好方案

| 列名 | 字段 | 类型 | 必须 | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | Y |  |
| 组织类型 | type | BYTE | Y | 组织架构，组 |
| 组织 | org_id | LONG | N |  |
| 职位 | position | VARCHAR(50) | N |  |
| 角色 | role_id | LONG | Y |  |

# 业务需求
## 权限
1. 角色只可分配自己的权限
1. 组的用途：数据权限，任务分配，申请借阅
1. 报告上有级别字段
1. 主任和科员，区别在报告查看级别

## 医院
1. 组织架构：医院 -> 院区 -> 科室
1. 病区，工作站：都只是信息

# 资料
## 参考
* [数据和界面参考](https://gitee.com/shuzheng/zheng)
* [RBAC新解：基于资源的权限管理(Resource-Based Access Control)](http://globeeip.iteye.com/blog/1236167)

## Spring Security
* [Spring Security参考手册](https://springcloud.cc/spring-security-zhcn.html)
* [234390216的博客 - spring Security分类文章列表](http://elim.iteye.com/category/182468)
* [Spring boot 和Spring Security4最新整合实例](https://wenku.baidu.com/view/14f0efb8ee06eff9aef807c0.html#%23%23)
* [Spring Security基于表达式的权限控制](http://elim.iteye.com/blog/2247073)
* [使用Spring Security进行Spring MVC的权限验证](https://www.tianmaying.com/tutorial/spring-security)

## Thymeleaf
* [thymeleaf-extras-springsecurity4](https://github.com/thymeleaf/thymeleaf-extras-springsecurity)
* [Thymeleaf + Spring Security integration basics](https://www.thymeleaf.org/doc/articles/springsecurity.html)
* [Thymeleaf: check if the user is authenticated with Spring Security](http://blog.netgloo.com/2015/03/01/thymeleaf-check-if-the-user-is-authenticated-with-spring-security/)

## Shiro
* [springboot(十四)：springboot整合shiro-登录认证和权限管理 - 纯洁的微笑博客](http://www.ityouknow.com/springboot/2017/06/26/springboot-shiro.html)
* [Spring Boot Shiro权限管理【从零开始学Spring Boot】](http://412887952-qq-com.iteye.com/blog/2299777)
* [Shiro 使用详解](https://juejin.im/entry/5788f6842e958a005419e22a)
* [权限验证框架Shiro使用详解](https://blog.csdn.net/xiaokang123456kao/article/details/72910806)
