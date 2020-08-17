#七牛

## 文件上传
1. 上传文件到测试服务器
1. 用postman执行
```
http://ljapi.swao.cn/qiniu/file/upload
{
  "type":"server",
  "filePath":"/opt/longjing/data/file/pc.png", // 测试服务器上的路径
  "remotePath":"ttt/1.png" // 七牛的路径
}
```

## 缓存刷新
1. 用postman执行
```
http://ljapi.swao.cn/qiniu/file/refresh
{
  "urls": ["https://s.swao.cn/ttt/defaultHeader.jpg"], // 可选，文件网址最多100个
  "dirs": ["https://s.swao.cn/ttt"] // 可选，路径网址最多10个
}
```

## 资料
* [Postman使用](http://blog.csdn.net/u013613428/article/details/51577209)
