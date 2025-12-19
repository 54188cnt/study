# 一、Swagger
[官网](https://swagger.org.cn/docs/)  
Knife4j是为Java MVC框架集成的Swagger生成API文档的增强解决方案  

步骤：  
- 创建WebMvcConfiguration配置类

常用注解：
- <font color="YELLOW">@Tag</font>: 类上(controller), 表示对类的说明
- <font color="YELLOW">@Schema</font>: 类上(entity, dto, vo), 表示对类用途的说明
- <font color="YELLOW">@Schema</font>: 属性上, 描述属性信息
- <font color="YELLOW">@Operation</font>: 方法上(controller的方法上), 说明方法的用途、作用

# 二、基础业务

## 2.1 购物车功能

### 清除购物车
购物车的数据存储在 redis 里面，便于清理，但是清除购物车的时候就会出现BigKey问题
```java
// 解决方式：不使用 delete, 使用unlink
public void clean() {  
    String cartKey = RedisConstant.SHOPPING_CART_KEY + UserHolder.getCurrentId();  
    // stringRedisTemplate.delete(cartKey);  
    stringRedisTemplate.unlink(cartKey);
}
```

### 添加商品到购物车
使用Hash数据结构，以`[dishId ? 0]:[setmealId ? 0]:[dishFlavor ? none]` 作为 field , value 表示的是物品数量  

### 删除购物车商品
删除的时候数据变化与删除 field 是异步的，并发状态下会导致问题，可以使用 Lua 脚本进行优化
```java
public void sub(CartDTO cartDTO) {  
    String cartKey = RedisConstant.SHOPPING_CART_KEY + UserHolder.getCurrentId();  
    String field = buildField(cartDTO);   
    // 下面这个会在高并发出现问题
    /*
    String val = (String) stringRedisTemplate.opsForHash().get(caryKey, field);
    if(val == null) return ;
    long num = Long.valueOf(val);
    if(num > 1) {
	    stringRedisTemplate.opsForHash().increment(cartKey, field, -1);
    }else {
	    stringRedisTemplate.opsForHash().delete(cartKey, field);
    }
    */
    
    Long res = stringRedisTemplate.opsForHash().increment(cartKey, field, -1); 
    // TODO 若是redis出现问题会导致出现脏数据  
    if(res <= 0) {  
        stringRedisTemplate.opsForHash().delete(cartKey, field);  
    }  
}
```

Lua脚本：
```lua
local count = redis.call('HINCRBY', KEYS[1], ARGV[1], -1)
if count <= 0 then
	redis.call('HDEL', KEYS[1], ARGV[1])
end
return count
```

运行脚本：
```java
stringRedisTemplate.execute(
	new DefaultRedisScript<>(luaScript,Long.class),
	Collections.singletonList(cartKey), 
	field
);
```

### 查看购物车商品
由于商品很多，一个一个的去查会浪费大量时间，可以分为查询菜品和查询套餐，通过集合查询去一次性拉出来，最后在逐个处理
[Collectors学习](Java进阶学习/Collectors.md) 








