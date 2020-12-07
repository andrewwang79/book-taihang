# 缓存
* 缓存存储采用redis

## 类型
1. 实体数据(DB)：单表，一般和dao一致
1. 业务数据：多表关联，关联度广。

| 类型 | 实例 | 说明 |
| :----: | ---- | ---- |
| 实体数据 | CRUD，查询 |  |
| 业务数据-业务 | 首页 | 依赖于实体数据 |
| 业务数据-搜索 |  | 可以通过第三方搜索服务(如ElasticSearch)来实现 |

## 方案
### 业务数据方案
1. 周期更新。周期自动重新生成缓存，无效上一次的缓存。如首页自动一小时更新一次。
1. 调整更新。关联数据无效后，才无效缓存。需要指定关联情况，比较复杂。

### 实体数据间的关联缓存
* 如用户好友列表和好友信息
* 尽量不要做关联，只做key关联。比如用户好友列表只记录好友id，这样好友信息修改后不会关联。

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

## 代码
### 规则
1. 每个cache都有实体和业务两种缓存类型
1. CRUD函数需配置cache
1. 涉及多实体的函数（如多表关联、使用了其他service的函数），要依赖自身缓存和关系业务缓存。如我的小区返回小区列表，需要同时配置“我的小区”和“小区”
1. 无dao的函数，无需配置cache
1. 有dao或者CRUD的public函数，都必须配置cache。读取的用CACHE_BIZ，其他的同CUD
1. 有dao但不是R操作的函数，需使用service的CRUD，不能使用dao

### 实例
```Java
NewsDao:
private CACHE_ENTITY = "News"; // 实体缓存
public CACHE_BIZ = "NewsBiz"; // 业务缓存

@CacheEvict(value = CACHE_BIZ, allEntries = true)
create()

@Cacheable(value = CACHE_ENTITY, key = "CACHE_ENTITY + #id")
get()

@CachePut(value = CACHE_ENTITY, key = "CACHE_ENTITY + #id")
@CacheEvict(value = CACHE_BIZ, allEntries = true)
update()

@CacheEvict(value = CACHE_ENTITY, key = "CACHE_ENTITY + #id")
@CacheEvict(value = CACHE_BIZ, allEntries = true)
delete()

NewsService：
@Cacheable(value = NewsDao.CACHE_BIZ, key = "NewsDao.CACHE_BIZ + 'TOP3' + #p1 + #p2")
getTop3() // 单表关联

@Cacheable(value = (NewsDao.CACHE_BIZ, CategoryDao.CACHE_BIZ), key = "NewsDao.CACHE_BIZ + 'TOP5' + #p1 + #p2")
getTop5() // 多表关联
```

PageImpl都是boss用的，要缓存用CustomPageImpl，因为类反序列化需要有默认构造函数。
