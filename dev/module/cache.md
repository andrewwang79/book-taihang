# 缓存


---
## 使用缓存
1. [缓存用spring的缓存](http://blog.csdn.net/partner4java/article/details/8600666)
2. 在业务层使用缓存


## 方案
1. 块以实体的名字命名
2. 每个实体service中的缓存块有两个，一个是用于CRUD缓存，一个是用于业务数据操作的缓存
3. 单个实体的缓存，对数据库有修改的删除业务缓存,更新CRUD缓存，读取时加入缓存
4. 关联数据的缓存依托于单个实体的缓存，当某个实体的缓存失效后，关联数据的缓存全部失效

## 具体操作
1. 单个块的操作：create,update,delete被视为修改了数据，更新CRUD缓存，删除所在块的业务缓存的所有内容;read，读取数据，在两个块中添加缓存(例：CommunityService）

2. 多个块的关联操作：一个业务方法中用到多个块的数据，缓存这个方法结果要同时属于这几个块，那么这个业务方法的结果就依赖于单个块的操作。（例：MtManager）
## 注意：
1. 需要缓存的入参实体需要手动写key， key的命名：key='业务块类型'+#entity.id

2. 加了缓存的方法调用要在不同类中（cache是基于动态生成的 proxy代理机制来对方法的调用进行切面，如果对象的方法是内部调用（即 this 引用）而不是外部引用，则会导致 proxy 失效）

3. 缓存放在业务层

## 例子
```
    public final static String CACHE_ENTITY = "community.";
    public final static String CACHE_BIZ = "communityBiz.";

    @Override
    @CacheEvict(value = CACHE_BIZ, allEntries = true)
    public Community create(Community obj) {
        obj.setStatus(StatusEnum.VALID.getValue());
        obj.setCreatetime(new Date());
        return this.communityDao.save(obj);
    }

    @Override
    @Caching(cacheable = { @Cacheable(value = CACHE_ENTITY, key = "'" + CACHE_ENTITY + "'+#id"), @Cacheable(value = CACHE_BIZ, key = "'" + CACHE_ENTITY + "'+#id") })
    public Community read(String id) {
        return this.communityDao.findOne(Long.parseLong(id));
    }

    @Override
    @Caching(put = { @CachePut(value = CACHE_ENTITY, key = "'" + CACHE_ENTITY + "'+#obj.id") }, evict = { @CacheEvict(value = CACHE_BIZ, allEntries = true) })
    public Community update(Community obj) {
        return this.communityDao.save(obj);
    }

    @Override
    @Caching(evict = { @CacheEvict(value = CACHE_ENTITY, key ="'" + CACHE_ENTITY + "'+#obj.id"), @CacheEvict(value = CACHE_BIZ, allEntries = true) })
    public Community delete(Community obj) {
        obj.setStatus(StatusEnum.DELETE.getValue());
        return this.communityDao.save(obj);
    }

    @Cacheable(CACHE_BIZ)
    public Community getByNameAndAddress(String name, String address) {
        return this.communityDao.getByNameAndAddress(name, address);
    }
```
