# 报表

## 类型
1. 常规报表
1. 结余报表(balance)：特殊报表，有期初期末
1. 账单：特殊报表

## 表结构(th_report)
* 商户类型和编号都为null，代表平台

| 列名 | 字段 | 类型 | NULL | 说明 |
|:--------:|:--------:|:--------:|:--------:|:--------:|
| 编号 | id | LONG | N | |
| 商户类型 | merchant_type | VARCHAR(100) | Y | 商城，ERP等 |
| 商户 | merchant_id | LONG | Y | 商户号null代表平台：比如type是平台的商户服务费，目标对象是商户 |
| 目标类型 | target_type | VARCHAR(100) | N | 商户销售统计，门店销售统计，库存货品结余，资金结余等 |
| 目标对象 | target_id | LONG | N | 如商户(商户销售统计)/门店(门店销售统计)/仓库(仓库库存货品结余)/门店(资金结余) |
| 标题 | title | VARCHAR(200) | N | 报表名称+参数1+参数n。如 "月销售统计-XX商户-201707" |
| 开始时间 | start_time | DATE | N | |
| 结束时间 | end_time | DATE | N | |
| 数据版本 | data_version | LONG | N | 默认是1 |
| 数据 | data | TEXT | N |  |
| 文件下载链接 | file_url | VARCHAR(1024) | Y |  |
| 创建时间 | createtime | DATE | N | |

## 报表数据的json推荐结构
```java
class ReportData {
  Map<String> summary; // 概要，预置json字段名是s_summary
  List<ReportDataItem> list; // 列表项，预置json字段名是s_list
  String initialData; // 期初数据，预置json字段名是s_initial
  String inData; // 入的数据，预置json字段名是s_in
  String outData; // 出的数据，预置json字段名是s_out
  String balanceData; // 期末/结余数据，预置json字段名是s_balance
}
class ReportDataItem {
  Map<String> data; // 数据
  String initialData; // 期初数据，预置json字段名是s_initial
  String inData; // 入的数据，预置json字段名是s_in
  String outData; // 出的数据，预置json字段名是s_out
  String balanceData; // 期末/结余数据，预置json字段名是s_balance
}
```
所有的String都可能是json或者字符串
