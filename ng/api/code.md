# 返回码
## 范围
| 项 | 定义 | 说明 |
| :----: | ---- | ---- |
| 0 | 请求成功 |  |
| -1 | 系统繁忙 |  |
| 1-499 | 通用系统错误 |  |
| 500-999 | 通用业务错误 |  |
| 1000以上 | 自定义业务错误 | 业务系统自行定义使用 |

## 定义
### 成功
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 0 | 成功 | SUCCESS |

### 系统
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| -1 | 繁忙  | BUSY |
| 1 | 失败 | FAIL |
| 2 | 资源锁定失败 | LOCK_FAIL |
| 3 | 无可用资源 | NO_RESOURCE |

### 接口
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 50 | 无接口 | NO_METHOD |
| 51 | 无权限 | NO_PERMISSION |
| 52 | 接口废弃 | DEPRECATED |
| 53 | 操作频繁 | OPERATION_FAST |
| 54 | 超过最大尝试次数 | MAX_TRY |

### 输入参数检查
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 80 | 参数缺失 | PARAM_MISS |
| 81 | 参数错误 | PARAM_ERROR |
| 82 | 参数长度错误 | PARAM_LENTH_ERROR |
| 83 | 参数格式错误 | PARAM_FORMAT_ERROR |

### 业务处理
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

### 账号权限
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

### 文件系统
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| 900 | 目录不存在 | NO_DIR |
| 901 | 目录为空  | EMPTY_DIR |
| 905 | 目录已存在  | EXIST_DIR |
