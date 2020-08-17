# 数据库

# 资金管理

## 账户表(th_finance_account)

| 列名 | 字段 | 类型 | 说明 |
| --------   | -----:  | :----:  |  :----:  |
| id | id | long |  |
| 目标类型 | target_type | VARCHAR(50) | 目标类型：商户，服务员 |
| 目标id | target_id | long |  |
| 总金额 | amount | bigDecimal(15,2)  |  |
| 冻结金额 | freeze_amt|bigDecimal(15,2) |可提现金额 = 总金额 - 冻结金额，冻结金额初始化为0.00元|
| 修改时间 | update_time|date|  |
| 创建时间 | createtime|date|  |
| 账户状态 | status|int|生效：1，冻结：2，注销：3|

## 账户明细表(th_finance_account_detail)

| 列名 | 字段 | 类型  |说明|
| --------   | -----:  | :----:  |  :----:  |
| id | id | long |  |
|  账户Id | account_id | long |  |
|  相关类型   | relevant_type | VARCHAR(50) |  |
| 相关Id   | relevant_id | long |  |
|  金额   | amount | bigDecimal(15,2) |  |
| 备注   | remark | VARCHAR(1000) |  |
| 创建时间  | createtime | Date |  |
| 状态   | status | int | |

## 提现表(th_finance_withdraw)

| 列名 | 字段 | 类型  |说明|
| --------   | -----:  | :----:  |  :----:  |
| id | id | long |  |
|  目标类型   | target_type | VARCHAR(50) |  |
| 目标Id   | target_id | long |  |
|  交易号  | trade_no | VARCHAR(100) | 打款流水号 |
|  提现方式  | method | VARCHAR(50) | WX,Alipay |
|  提现账号 | account | VARCHAR(50) |  |
|  金额   | amount | bigDecimal(15,2) |  |
| 备注   | remark | VARCHAR(1000) |  |
| 创建时间  | createtime | Date |  |
| 状态   | status | int | 申请中：1，打款中：2，提现成功：3，提现失败：4|

## 付款表

|列名|字段|类型|NULL|说明|
|:--------:|:--------:|:--------:|:--------:|:--------:|
|编号|id|LONG|N| |
|付款人类型|relevant_type|VARCHAR(50)|N| |
|付款账户Id|accountId|VARCHAR(50)|N| |
|付款凭证|pay_voucher|VARCHAR(50)|N| |
|付款金额|amt|BIGINT|N| |
|备注|remark|VARCHAR(500)|Y|  |
|确认付款|sure|boolean|N| |
|创建时间|createtime|DATE|N| |

## 服务收支(th_finance_biz_balance)
