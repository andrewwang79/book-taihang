# 开发规范

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

## API
* https://wiki.fosun.com/pages/viewpage.action?pageId=38682988

### 接口命名
* 格式 : 版本 + 业务(多层用/分隔) + 操作(用_分隔)
* 示例

| 操作 | 示例 | 说明 |
| :----: | -- | -- |
| 创建(C) | /v1/user/create |  |
| 读取(R) | /v1/user/read |  |
| 更新(U) | /v1/user/update |  |
| 删除(D) | /v1/user/delete |  |
| 查询 | /v1/user/query | 无分页 |
| 搜索 | /v1/user/search | 有分页 |
| 自定义操作 | /v1/user/batch_delete | 批量删除用户 |
| 多层业务-列表读取 | /v1/user/school/all | 获取用户所有学校 |
| 多层业务-自定义操作 | /v1/user/password/forget | 忘记密码 |

#### 常用的自定义操作

| 功能 | 编码 |
| :----: | -- |
| login | 登录 |
| logout | 登出 |
| list | 列表 |
| all | 所有 |
| batch_delete | 批量删除 |
| forget | 忘记 |
| reset | 重置 |
| import | 导入 |
| export | 导出 |
| check | 检查 |
| apply | 申请 |

### 返回结构
| 字段 | 名称 | 说明 |
| :----: | -- | -- |
| code | 返回码 | 用于成功和业务前置条件检查。前置条件错误的返回码如参数错误和数据已存在等 |
| msg | 消息 | 失败会返回本字段 |
| data | 结果 | 自定义json。业务执行结果。如返回create编号 |

### 返回码
* 1-499是通用系统错误
* 500-999是通用业务错误
* 1000以上是自定义业务错误，框架内只能定义1-999错误

#### 成功
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 0 | 成功 | SUCCESS |

#### 系统
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| -1 | 繁忙  | BUSY |
| 1 | 失败 | FAIL |
| 2 | 资源锁定失败 | LOCK_FAIL |
| 3 | 无可用资源 | NO_RESOURCE |

#### 接口
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 50 | 无接口 | NO_METHOD |
| 51 | 无权限 | NO_PERMISSION |
| 52 | 接口废弃 | DEPRECATED |
| 53 | 操作频繁 | OPERATION_FAST |
| 54 | 超过最大尝试次数 | MAX_TRY |

#### 输入参数检查
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 80 | 参数缺失 | PARAM_MISS |
| 81 | 参数错误 | PARAM_ERROR |
| 82 | 参数长度错误 | PARAM_LENTH_ERROR |
| 83 | 参数格式错误 | PARAM_FORMAT_ERROR |

#### 业务处理
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 400 | 数据不存在 | NOT_EXIST |
| 401 | 数据已存在 | EXIST |
| 402 | 数据重复 | DATA_DUP |
| 413 | 删除失败 | DELETE_ERROR |
| 414 | 创建失败 | CREATE_ERROR |
| 415 | 修改失败 | UPDATE_ERROR |
| 450 | 验证码错误 | CAPTCHA_ERROR |
| 451 | 验证码发送频繁 | CAPTCHA_SEND_FAST |
| 460 | 地址解析错误 | ADDRESS_PARSE_ERROR |

#### 账号权限
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 500 | 登录失败 | LOGIN_FAIL |
| 501 | 需登录  | NEED_LOGIN |
| 503 | 账户冻结 | ACCOUNT_FROZEN |
| 506 | 账户警告 | ACCOUNT_WARNING |
| 507 | 手机号已使用 | MOBILE_USED |
| 508 | 该账户已被禁用，请联系客服 | ACCOUNT_BAN |
| 509 | 该账号已完成绑定，请勿重复提交 | ACCOUNT_BIND |
| 510 | 微信和微信公众号不是同一个账号 | WX_USER_USED |
| 511 | 手机号不存在 | MOBILE_NOT_EXIST |
| 512 | 密码错误 | PWD_ERROR |
| 513 | 新旧密码相同 | SAME_PWD |
| 520 | 角色编码错误 | ROLE_CODE_ERROR |

#### 文件系统
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 900 | 目录不存在 | NO_DIR |
| 901 | 目录为空  | EMPTY_DIR |
| 905 | 目录已存在  | EXIST_DIR |

### token
所有API请求(除了登录等用户无关的)都必须有字段token，token通过login返回

### 分页
#### 输入
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| page | 页号 | 从1开始，默认是1 |
| pageSize | 每页个数 | 默认是10，默认是10，0是所有 |

#### 输出
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| total | 总个数 |  |
| pages | 总页数 |  |
| list | 数据列表 |  |

### 文档编写
```
### 用户下一个任务(/v1/task/user/next)
输入

| 名称 | 字段1 | 字段2 | 类型 | 必须 | 说明 |
| :----: | -- | -- | -- | -- | -- |
| 用户 | userId |  | INT | Y |  |

输出

| 名称 | 字段1 | 字段2 | 类型 | 必须 | 说明 |
| :----: | -- | -- | -- | -- | -- |
| 序列列表 | list |  | LIST(STRING) | Y |  |

返回码
```

### 代码编写
```
@RequestMapping("/create")
public ApiOutput create(@RequestBody String json) {
  log.info(LogUtil.gen("create", "json", json)); // log
  String name = ArrayUtil.getMapString(map, "name"); // 获取输入参数
  if (Strings.isNullOrEmpty(name) || name.length() > 50) { // 检查输入参数
      return new ApiOutput(ApiCodeEnum.PARAM_ERROR, "name");  // 基础返回码
  }

  ... 业务处理

  return new ApiOutput(SysApiCodeEnum.NO_SERIES_IN_TASK);  // 业务返回码

  int apiCode = annotationResultManager.submitSeriesAnnotationResult(id); // 业务层结果的返回码
  return new ApiOutput(apiCode);
}
```

### 使用事项
1. 返回结果的data里列表默认字段名称是list
1. 分隔符默认都是","
1. 传输默认时间：基于北京时间，传输使用字符串，格式"yyyyMMddHHmmss"

## 数据表
### 字段定义
| 功能 | 示例 | 说明 |
| :----: | -- | -- |
| 整数 | int |  |
| 名字等 | varchar(50) |  |
| 说明/网址 | varchar(1024) |  |
| 枚举(整数) | tinyint |  |
| 枚举(字符串) | varchar(20) |  |
| 金额 | decimal |  |
| 文字 | text |  |
| 布尔值 | bit |  |
| 时间 | datetime |  |

### 名词定义

## 编码
###
* 研发阶段和效率价值金字塔![](http://mmbiz.qpic.cn/mmbiz_png/JLT28M0ib5gBpm1W5WWhvpribW398AGxyFVEncRsGm6LayeIgfV3Qp9uxIMqKr5Jqhn6VcfrMerib14rgI7qlLvvQ/0?wx_fmt=png)
* [参考](https://andrewwang79.gitbooks.io/javadev/spec/coding.html)
* 先方案，再文档，最后代码

### 代码
1. 一个函数最多80行代码，建议30行
1. 事务只在manager层。[资料](http://www.importnew.com/19489.html)
1. json只在API层
1. 操作不能放在if里。for里可以

### UT
* 业务功能做UT
* 交叉做，团队

### log
1. 只能是英文，用LogUtil
1. 记录业务函数输入输出

### 注释
1. 代码自说明，能说明的不写注释
1. 核心逻辑全面覆盖注释

### 代码提交和git
* git : http://wangyaqi.cn/2015/05/18/git/
* 提交时间，提交前先拉取代码
  * 任务完成就提交
  * 每天下班前提交
* 提交内容：代码，sql，配置
* 代码合并

## 考虑
### 目标
1. 按照开发规范开发
1. 1个sprint延期任务(本人原因)不超过1个
1. 1个人天1个bug，S2的bug是1，S1是2，S3是0.5，S4是0.25

### 代码量和bug数
* 目标是解决，不是代码量对应的bug量
* 代码量：一般200行/1天，复杂是100行/1天

| 级别 | 千行代码Bug率 | 一般 | 复杂 | 说明 |
| :----: | -- | -- | -- | -- | -- |
| CMM1级 | 11.95‰ | 2.39 | 1.195 |  |
| CMM2级 | 5.52‰ |1.104 | 0.552 |  |
| CMM3级 | 2.39‰ | 0.478 | 0.239 |  |
| CMM4级 | 0.92‰ | 0.184 | 0.092 |  |
| CMM5级 | 0.32‰ | 0.064 | 0.032 |  |

### 任务统计
任务，人天，负责人，允许bug值，是否延期，bug数，bug值

### 分工
1. 系统负责人
  1. 准时完成全部开发测试(不含部署)
  1. 任务统计

1. 王亚琪
  1. 技术方案设计和评审
  1. 基础库维护
