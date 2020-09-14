# 缓存
## 缓存key规则
* 规则：分类_参数。

例如：
* 实体：id是1000的活动，event_1000
* 搜索结果：s_news-lastIndex-1-10-keyword。s_news-1200-1-10-iphone，新闻搜索结果，起始点是id是1200的新闻，第一页，每页是10个，关键字是iphone

## 流程
* 写：数据库
* 读：读缓存，没有读数据库(同时保存到缓存)

## 更新机制
使用缓存的自动过期机制
如有数据更新，可强制更新。如达到更新的最小条数minCount(如5个)

## 搜索
* 通过参数lastindex确保结果唯一
* 新增:系统周期的自动更新到lastindex
* 修改:对象动态自动更新
* 删除:自动过期机制

# 页面缓存
特别适用于微信的页面缓存机制（微信访问的第一个页面会做强制缓存，加随机数是无效的）

* index.html页面上有个加载js文件，在js文件中加随机数加载其他js配置文件（确保本文件每次都被重新加载），至于其他js文件，如果没有版本更新，无需加载新的。
* 每个js库有自身的版本号(config.js)，如有更新，版本号+1。
* 项目也有自身的版本号(index.html)，如有更新，版本号+1。
* 项目有版本信息(index.html的VERSION)，会和版本号一起更新。

## 注意
项目只有在正式环境下时，文件才有缓存。

## 文件替换注意事项
强制全覆盖。