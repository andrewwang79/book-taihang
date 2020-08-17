# 数据库

## 服务员
* 身份证，总收入，余额等
* 财务账户（用于结算）

## 收支记录
所属账单

## 账单
打款时间

## 服务商户 merchant
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 编码 | code | VARCHAR(255) | Y |  |
| 名称 | name | VARCHAR(500) | Y |  |
| 电话 | mobile | VARCHAR(50) | Y |  |
| 地址 | address | VARCHAR(255) | Y |  |
| 经度 | latitude | DECIMAL | Y |  |
| 纬度 | longitude | DECIMAL | Y |  |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 分类 | type | VARCHAR(50) | N | 个体/机构 |
| 创建时间 | createtime | DATE | N |  ||

## 分支机构 branch
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 服务商户id | merchantId | LONG | N |  |
| 编码 | code | VARCHAR(255) | Y |  |
| 名称 | name | VARCHAR(500) | Y |  |
| 地址 | address | VARCHAR(255) | Y |  |
| 经度 | latitude | DECIMAL | Y |  |
| 纬度 | longitude | DECIMAL | Y |  |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 分类 | type | VARCHAR(50) | N | 门店，子机构 |
| 营业状态 | operateStatus | Integer | N | |
| 创建时间 | createtime | DATE | N |  ||

## 分支机构服务 branch_service
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 分支机构id | branchId | LONG | Y |  为空表示属于商户 |
| 服务 | service_code | VARCHAR(50) | N |  |
| 服务配置 | service_config | TEXT | N |  |

## 员工 employee
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 名字 | name | VARCHAR(100) | Y |  |
| 头像 | headImage | VARCHAR(255) | Y |  |
| 电话 | mobile | VARCHAR(50) | N |  |
| 密码 | password | VARCHAR(100) | N |  |
| 员工状态 | service_status | VARCHAR(50) | Y |  正常，休假，离职|
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  ||

## 员工服务 employee_service
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 分支机构id | branchId | LONG | Y |  为空表示属于商户 |
| 员工id | employeeId | LONG | N |  |
| 服务 | service_code | VARCHAR(50) | N |  |
| 服务配置 | service_config | TEXT | N |  |

## 员工归属 employee_belong
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 服务商户id | merchantId | LONG | N |  |
| 分支机构id | branchId | LONG | Y |  为空表示员工属于商户 |
| 员工id | employeeId | LONG | N |  |
| 角色 | role | VARCHAR(50) | N | 负责人，店长，服务员 |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  ||

## 员工调动历史(employee_change_hs)
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 服务商户id | merchantId | LONG | N |  |
| 分支机构id | branchId | LONG | Y | 为空表示员工属于商户 |
| 员工id | employeeId | LONG | N |  |
| 员工调动状态 | change_status | VARCHAR(50) | Y |  入职，转职，离职 |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  ||

## 服务记录 service_record
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N |  |
| 服务商户id | merchantId | LONG | N |  |
| 分支机构id | branchId | LONG | N |  |
| 员工id | employeeId | LONG | N |  |
| 服务 | service | VARCHAR(50) | N |  物流，气象 |
| 服务类型 | service_type | VARCHAR(50) | N |  自提，代送，代购 |
| 服务工单 | service_order | VARCHAR(50) | N |  订单号，物流号 |
| 服务费 | service_fee | BigDecimal | N | |
| 说明 | remark | VARCHAR(1000) | Y |  |
| 创建时间 | createtime | DATE | N |  ||
