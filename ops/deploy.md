# 产品服务端部署

## 准备材料
1. 配置项增删改
1. 文件增删改。如excel导入模板
1. 表新建，表字段增删改
1. 表数据增删改

## 流程
* 单服务端系统需要设置成“升级中”，分布式系统无需设置。
* 前端在“升级中”状态时，需要有升级提示页面。
* “升级中”状态放在网络的一个独立位置，如官网的一个路径

## 注意事项
不能删除表，如有需要可修改表名，表名规则是"表名修改人日期"，如config_andrew_20161212。
