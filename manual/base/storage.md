# 存储服务

## 配置
| 名称 | 参数 | 默认值 |
| :----: | ---- | ---- |
| 七牛accessKey | th.qiniu.accessKey | 无 |
| 七牛秘钥 | th.qiniu.secretKey | 无 |
| 七牛空间 | th.qiniu.bucket | 无 |
| 七牛空间对应的网址 | th.qiniu.http.context | 无 |

## 函数
| 类 | 函数 | 输入 | 输出 | 说明 |
| :----: | ---- | ---- |
| QiniuController | /qiniu/uptoken | 无 | String uptoken | 获取上传token |
| QiniuController | /qiniu/file/upload/UEditor | UEditor原生上传的文件列表 | FileUploadResult | UEditor上传 |
| QiniuController | /qiniu/file/delete | String bucket, String key | boolean 删除成功 | 删除文件 |
| QiniuController | /qiniu/file/refresh | String[] urls(可选), String[] dirs(可选) | boolean 刷新成功 | CDN刷新。文件网址最多100个，路径网址最多10个 |
| QiniuService | uploadFile | String filePath, String bucket | String key | 上传文件，返回文件url(UUID格式) |
| QiniuService | uploadFileByName | String filePath, String fileName | String key | 上传文件，返回文件url |
| QiniuService | delete | String bucket(null使用配置值), String key | boolean 删除成功 | 删除文件 |

## 使用
### API
```JavaScript
/qiniu/file/delete
{
  "bucket": null, "key": "cefc7118-bcae-4915-b24f-eeab4075f172"
}

/qiniu/file/refresh
{
  "urls":["http://s.xyz.com/cefc7118-bcae-4915-b24f-eeab4075f172"],
  "dirs":["http://s.xyz.com/image/"]
}
```

### 代码
```Java
@Autowired
private QiniuService qiniuService;

this.qiniuService.uploadFile("c:/123.jpg", null);
this.qiniuService.uploadFileByName("c:/123.jpg", "img/123.jpg");
this.qiniuService.delete(null, "img/123.jpg");

```

## 说明
* 当前实现了七牛
* 返回全路径url
* [方案设计](./design/base/storage.html)
