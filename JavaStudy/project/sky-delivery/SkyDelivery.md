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
[Collectors学习](../../Java进阶学习/Collectors.md) 

## 2.2 订单相关功能

### 生成唯一订单ID
```java
public class SnowflakeIdGenerator {  
  
    // 起始时间戳 (例如：2023-01-01)，一旦确定不可修改  
    private final long twepoch = 1672531200000L;  
  
    // 各部分占用的位数  
    private final long workerIdBits = 5L;   // 机器标识占用的位数  
    private final long datacenterIdBits = 5L; // 数据中心占用的位数  
    private final long sequenceBits = 12L;  // 序列号占用的位数  
  
    // 各部分最大值 (位运算计算)  
    private final long maxWorkerId = ~(-1L << workerIdBits);  
    private final long maxDatacenterId = ~(-1L << datacenterIdBits);  
    private final long sequenceMask = ~(-1L << sequenceBits);  
  
    // 各部分向左移位的位数  
    private final long workerIdShift = sequenceBits;  
    private final long datacenterIdShift = sequenceBits + workerIdBits;  
    private final long timestampLeftShift = sequenceBits + workerIdBits + datacenterIdBits;  
  
    private long workerId;        // 工作机器ID  
    private long datacenterId;    // 数据中心ID  
    private long sequence = 0L;   // 毫秒内序列  
    private long lastTimestamp = -1L; // 上次生成ID的时间戳  
  
    public SnowflakeIdGenerator(long workerId, long datacenterId) {  
        if (workerId > maxWorkerId || workerId < 0) {  
            throw new IllegalArgumentException("worker Id can't be greater than maxWorkerId");  
        }  
        if (datacenterId > maxDatacenterId || datacenterId < 0) {  
            throw new IllegalArgumentException("datacenter Id can't be greater than maxDatacenterId");  
        }  
        this.workerId = workerId;  
        this.datacenterId = datacenterId;  
    }  
  
    // 核心方法：生成ID (线程安全)  
    public synchronized long nextId() {  
        long timestamp = timeGen();  
  
        // 检查时钟回拨  
        if (timestamp < lastTimestamp) {  
            throw new RuntimeException("时钟回拨，拒绝生成ID");  
        }  
  
        // 如果是同一毫秒内生成的，则进行毫秒内序列自增  
        if (lastTimestamp == timestamp) {  
            sequence = (sequence + 1) & sequenceMask;  
            // 毫秒内序列溢出  
            if (sequence == 0) {  
                // 阻塞到下一个毫秒,获得新的时间戳  
                timestamp = tilNextMillis(lastTimestamp);  
            }  
        } else {  
            // 时间戳改变，毫秒内序列重置  
            sequence = 0L;  
        }  
  
        lastTimestamp = timestamp;  
  
        // 通过位运算拼装成 64 位 ID        
        return ((timestamp - twepoch) << timestampLeftShift) // 时间戳差值左移  
                | (datacenterId << datacenterIdShift)         // 数据中心左移  
                | (workerId << workerIdShift)                 // 机器ID左移  
                | sequence;                                   // 序列号  
    }  
  
    protected long tilNextMillis(long lastTimestamp) {  
        long timestamp = timeGen();  
        while (timestamp <= lastTimestamp) {  
            timestamp = timeGen();  
        }  
        return timestamp;  
    }  
  
    protected long timeGen() {  
        return System.currentTimeMillis();  
    }  
}
```

### RedisUtils
这个代码只针对string类型，一般都
```java
public class RedisUtils {  
    private StringRedisTemplate redisTemplate;  
    private ObjectMapper objectMapper;  
  
    /**  
     * 写入缓存（永久有效）  
     */  
    public void set(String key, Object value) {  
        set(key, value, -1, TimeUnit.SECONDS);  
    }  
  
    /**  
     * 写入缓存（设置过期时间）  
     */  
    public void set(String key, Object value, long timeout, TimeUnit unit) {  
        try {  
            String val = toJson(value);  
            if (timeout > 0) {  
                redisTemplate.opsForValue().set(key, val, timeout, unit);  
            } else {  
                redisTemplate.opsForValue().set(key, val);  
            }  
        } catch (Exception e) {  
            log.error("Redis set error! key: {}, error: {}", key, e.getMessage());  
        }  
    }  
  
    /**  
     * 获取对象  
     */  
    public <T> T get(String key, Class<T> clazz) {  
        String val = redisTemplate.opsForValue().get(key);  
        if (!StringUtils.hasText(val)) return null;  
        return fromJson(val, clazz);  
    }  
  
    /**  
     * 获取复杂类型（如 List<User>）  
     * 调用示例：List<User> list = redisUtils.get("userList", new TypeReference<List<User>>(){});  
     */    
     public <T> T get(String key, TypeReference<T> typeReference) {  
        String val = redisTemplate.opsForValue().get(key);  
        if (!StringUtils.hasText(val)) return null;  
        try {  
            return objectMapper.readValue(val, typeReference);  
        } catch (JsonProcessingException e) {  
            log.error("Redis get error! key: {}, error: {}", key, e.getMessage());  
            return null;  
        }  
    }  
  
    /**  
     * 删除 key  
     */    
     public Boolean delete(String key) {  
        return redisTemplate.delete(key);  
    }  
  
    /**  
     * 设置过期时间  
     */  
    public Boolean expire(String key, long timeout, TimeUnit unit) {  
        return redisTemplate.expire(key, timeout, unit);  
    }  
  
    // --- 内部辅助转换方法 ---  
    private String toJson(Object value) throws JsonProcessingException {  
        if (value == null) return null;  
        if (value instanceof String) return (String) value;  
        return objectMapper.writeValueAsString(value);  
    }  
  
    private <T> T fromJson(String json, Class<T> clazz) {  
        try {  
            if (clazz == String.class) {  
                return clazz.cast(json);  
            }  
            return objectMapper.readValue(json, clazz);  
        } catch (JsonProcessingException e) {  
            log.error("Json parse error! error: {}", e.getMessage());  
            return null;  
        }  
    }  
}
```

### RedisConfig
```java
public class RedisConfig {  
  
    @Bean  
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {  
        RedisTemplate<String, Object> template = new RedisTemplate<>();  
        template.setConnectionFactory(factory);  
  
        // 1. 使用 JSON 序列化器  
        GenericJackson2JsonRedisSerializer jsonSerializer = new GenericJackson2JsonRedisSerializer();  
  
        // 2. Key 始终使用 String 序列化  
        StringRedisSerializer stringSerializer = new StringRedisSerializer();  
  
        // 全局配置：Key 和 HashKey 用 String        template.setKeySerializer(stringSerializer);  
        template.setHashKeySerializer(stringSerializer);  
  
        // 全局配置：Value 和 HashValue 用 JSON        // 这样你存 List<User> 或 Map<String, Dish> 都能自动转 JSON 并带上类型  
        template.setValueSerializer(jsonSerializer);  
        template.setHashValueSerializer(jsonSerializer);  
  
        template.afterPropertiesSet();  
        return template;  
    }  
  
    // 专门为 Spring Cache 注解配置序列化  
    @Bean  
    public RedisCacheConfiguration redisCacheConfiguration() {  
        return RedisCacheConfiguration.defaultCacheConfig()  
                .entryTtl(Duration.ofHours(1)) // 设置默认过期时间  
                // 设置 Key 的序列化  
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()))  
                // 设置 Value 的序列化（使用带类型的 JSON，这样拿出来不用手动转）  
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(new GenericJackson2JsonRedisSerializer()))  
                .disableCachingNullValues(); // 不缓存空值  
    }  
}
```


