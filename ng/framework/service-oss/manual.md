# 使用

## 断点续传命令
java -jar oss-sdk-client.jar -host http://172.16.1.100  -filePath D:\file.zip   -resourceKey file.zip

| 字段 | 名称 | 说明 |
| :-: | - | - |
| host | oss服务地址 |  |
| filePath | 上传文件的本地路径 |  |
| resourceKey | 资源key | 上传文件存储路径 = oss数据路径 + resourceKey <br> 如oss数据路径为/oss/data，resourceKey为file.zip，则文件存储路径为/oss/data/file.zip |
