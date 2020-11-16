# API规范
* 接口输入输出 : https://taihang.wangyaqi.cn/#/spec/api
* [返回码](code)
* [示例](example)

## 接口命名
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

### 常用的自定义操作

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

## token
所有API请求(除了登录等用户无关的)都必须有字段token，token通过login返回

## 分页
### 输入
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| page | 页号 | 从1开始，默认是1 |
| pageSize | 每页个数 | 默认是10，默认是10，0是所有 |

### 输出
| 编码 | 名称 | 说明 |
| :----: | -- | -- |
| total | 总个数 |  |
| pages | 总页数 |  |
| list | 数据列表 |  |

## 字段定义
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

## 使用事项
1. 返回结果的data里列表默认字段名称是list
1. 分隔符默认都是","
1. 传输默认时间：基于北京时间，传输使用字符串，格式"yyyyMMddHHmmss"
