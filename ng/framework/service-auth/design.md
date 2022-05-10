# 设计
## 概要
* 基于RBAC授权和基于用户授权的细粒度权限控制通用平台，并提供单点登录、会话管理和日志管理。
* 接入的系统可自由定义组织、角色、权限、资源等。用户权限=所拥有角色权限合集+用户加权限-用户减权限，优先级：用户减权限>用户加权限>角色权限

## 原则
1. 职位只是信息，和权限无关
1. 将所有业务定义成权限
1. 权限可以分配给角色，不能分配给人
1. 1个用户可有多个角色，暂不支持继承(权限/角色)
1. 角色可以分配给人或组
1. 组和组织架构是独立的两个概念
1. 权限可以分配到组织架构&职位，组&职位

## 权限
* 权限无类型
* 实例：订单查看，订单修改，订单打印，报告打印等

## 权限清单
1. 用户角色权限
1. 用户所在组织架构
1. 用户所在组织架构的职位
1. 用户所在组
1. 用户所在组的职位

用户权限可缓存，在其对应关系有调整时重新计算并缓存

## 数据权限设计
1. 不同业务功能是不同页面和权限。比如对于报告，有3个页面：查看部门报告(部门经理)，查看部门报告(普通职员)，查看本人报告
1. 报告安全等级是权限，不同的角色有不同的等级权限
1. 某个科室的数据查看是权限，通过组赋予本权限

## 菜单
1. 1个权限对应N个可启用的菜单
1. 1个菜单启用最多只需要1个权限

## 页面
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

## API
* 数据关联机制保障权限：不能查看其权限无关的信息
* 使用：@RequiresPermissions("RESOURCE:VIEW")
* 暂不开发

## 组的权限设计
1. 把权限授权给组，组中的用户/机构就自动拥有这些角色/权限
1. 实例
  1. 影像数据管理员(角色)的权限 = 组管理员 + 影像数据管理
  1. 行政数据管理(角色)的权限 = 组管理员 + 行政数据管理
  1. 组员1的角色 = 组员 + 影像数据查阅

## 组织架构
1. 结构：公司 -> 部门(允许多层) -> 员工
1. 部门只能属于1个公司
1. 1个员工只有1个职位
1. 1个员工可属于多个部门

## 操作分工
### 运营人员
1. 用户管理，分配角色到用户
1. 角色管理，分配权限到角色
1. 权限和菜单配置
1. 组织架构管理

### 超级管理员
1. 权限编辑

# 资料
## 参考
* [数据和界面参考](https://gitee.com/shuzheng/zheng)
* [RBAC新解：基于资源的权限管理(Resource-Based Access Control)](http://globeeip.iteye.com/blog/1236167)
* https://www.cnblogs.com/butterfly100/p/8698425.html
* 功能
  * 垂直权限（功能权限）
  * 水平权限（数据权限）

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
