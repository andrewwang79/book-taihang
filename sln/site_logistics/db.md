# 数据库(桐庐)

# 数据库

## 供应商(tonglu_logistics_vendor)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 名称 | name | VARCHAR(200) | N |  |
| 类型 | type | VARCHAR(50) | N | 企业/个人 |
| 服务类型 | service_type | INT | N | 自提，配送 |
| 创建时间 | createtime | DATE | N |  |
| 状态 | service_status | INT | N | 停业 |

## 物流站点(tonglu_logistics_site)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 供应商编号 | vendor_id | Long | N | 供应商编号 |
| 业务id | biz_id | Long | N | 供应商站点编号 |
| 地址 | address | VARCHAR(200) | N |  |
| 纬度 | latitude | DECIMAL(19,11) | N |  |
| 精度 | latitude | DECIMAL(19,11) | N |  |
| 服务类型 | service_type | INT | N | 自提，配送 |
| 创建时间 | createtime | DATE | N |  |
| 状态 | service_status | INT | N | 停业？ |

## 快递员(tonglu_courier)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 物流站点 | logistics_site_id | Long | N |  |
| 业务id | biz_id | Long | N | 供应商员工编号 |
| 名称 | name | VARCHAR(50) | N |  |
| 性别 | sex | INT | N |  |
| 联系方式 | phone | VARCHAR(50) | N |  |
| 头像 | head_image | VARCHAR(100) | N |  |
| 备注 | remark | VARCHAR(100) | N |  |
| 配送日期 | deliver_day | INT | N | all=1, workday=2, weekend=4 |
| 配送时间 | deliver_time | INT | N | all=1, morning=2, afternoon=4, night=8 |
| 服务状态 | service_status | VARCHAR(100) | N | 同员工 |
| 服务类型 | service_type | INT | 自提，配送 |  |
| 创建时间 | createtime | DATE | N |  |

## 物流站点订单(tonglu_logistics_site_order)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 物流站点 | logistics_site_id | Long | N |  |
| 订单号 | order_id | Long | N |订单号 |
| 配送日期 | deliver_day | INT | N | all=1, workday=2, weekend=4 |
| 配送时间 | deliver_time | INT | N | all=1, morning=2, afternoon=4, night=8 |
| 服务类型 | service_type | INT | 自提，配送 |  |
| 创建时间 | createtime | DATE | N |  |

## 物流站点服务工单(tonglu_logistics_service_order)

| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 物流站点 | logistics_site_id | Long | N |  |
| 快递员 | courier_id | Long | N |  |
| 业务id | biz_id | Long | Y | 物流单号 |
| 服务类型 | service_type | INT | 自提，配送 |  |
| 提货码 | pick_code | VARCHAR(100) | Y |  |
| 服务状态 | service_status | VARCHAR(100) | N |  |
| 服务费 | service_fee | DECIMAL(16,2) | N |  |
| 收件人 | consignee_name | VARCHAR(100) | N |  |
| 配送时间 | consignee_time | VARCHAR(100) | N |  |
| 联系人电话 | consignee_phone | VARCHAR(100) | N |  |
| 联系人地址 | consignee_address | VARCHAR(100) | N |  |
| 下次状态调整时间 | next_status_time | DATE | N |  |
| 创建时间 | createtime | DATE | N |  |

## 供应商站点
* 服务范围：如上海市，上海市黄浦区
