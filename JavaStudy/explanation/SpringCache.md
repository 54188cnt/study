## Maven导入
```xml
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-cache</artifactId>  
</dependency>
```

****
## 常用注解
- <font color="yellow">@EnableCaching</font>: 开启缓存注解功能，通常加在启动类上
- <font color="yellow">@Cacheable</font>: 方法执行前查询缓存是否有数据，没有数据则调用方法将其返回值方式到缓存
- <font color="yellow">@CachePut</font>: 将方法的返回值放到缓存中
- <font color="yellow">@CacheEvict</font>: 将一条或多条数据从缓存中删除

### @CachePut
```java
@CachePut(cacheNames = "xxxCache", key = "#user.id")
// 或者 key = "#result.id"
// 或者 key = "#p0.id"
public User save(User user){
	userMapper.insert(user);
	return user;
}

// Redis的key为xxxCache::{id}
```

### @Cacheable
```java
@Cacheable(cacheNames = "xxxCache", key = "#id")
public User getById(Long id) {
	User user = userMapper.getById(id);
	return user;
}
```

### @CacheEvict
```java
@CacheEvict(cacheNames = "xxxCache", key = "#id")
public void deleteById(Long id) {
	userMapper.deleteById(id);
}

@CacheEvict(cacheNames = "xxxCache", allEntries = true)
public void deleteAll() {
	userMapper.deleteAll();
}
```