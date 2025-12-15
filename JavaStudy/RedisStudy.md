# 一、redis数据结构  

Redis是一个key-value的数据库，key是字符串类型，value可以是多种数据结构类型。  
value: String(字符串), List(列表), Set(集合), Hash(哈希), SortedSet(有序集合), 
Bitmap(位图), HyperLog(基数统计), GEO(地理位置)  
[redis官方文档](https://redis.io/docs/)  

## 1.1 redis命令
[redis命令参考](https://redis.io/commands/)  

通用命令  
`KEYS pattern` 查找所有符合给定模式的key    
`DEL key [key ...]` 删除一个或多个key  
`EXISTS key [key ...]` 检查给定key是否存在  
`EXPIRE key seconds` 设置key的过期时间，单位为秒  
`TTL key` 获取key的剩余生存时间，单位为秒
****  

string类型   
value是字符串类型，最大512MB，又可以分为int, float, string三种类型  
常见命令：SET, GET, MSET, MGET, INCR, INCRBY, DECR, DECRBY, INCRBYFLOAT, SETNX, SETEX  
<font color="yellow">层级格式</font>：[公司名]:[业务名]:[类型名]:id
****  

Hash类型  
value是一个键值对集合，适合存储对象  
常见命令：HSET, HGET, HMSET, HMGET, HGETALL, HKEYS, HVALS, HINCRBY, HSETNX
****  

List类型  
value是一个字符串列表，按插入顺序排序，适合存储消息队  
常见命令：LPUSH, RPUSH, LPOP, RPOP, LRANGE, BLPOP, BRPOP
****  

Set类型  
value是一个字符串集合，元素唯一且无序，适合存储标签、分类  
常见命令：SADD, SREM, SMEMBERS, SISMEMBER, SCARD, SINTER, SUNION, SDIFF
****

SortedSet类型  
value是一个带有分数的字符串集合(score, 存储时必须携带这个字段)，元素唯一且有序，适合存储排行榜、优先级队列  
常见命令：ZADD, ZREM, ZRANGE, ZRANGEBYSCORE, ZSCORE, ZRANK, ZCARD, ZCOUNT, ZINCRBY, ZDIFF, ZINTER, ZUNION

## 1.2 redis客户端  
### 1.2.1 Jedis
[Jedis官网](https://github.com/redis/jedis)  
使用步骤：  
1. 添加依赖  
2. 创建Jedis对象，连接redis服务器
3. 使用Jedis对象执行redis命令(指令同Redis指令)
****  

Jedis连接池  
1. 创建工厂类JedisConnectionFactory，配置连接池参数  
``` java
public class JedisConnectionFactory {
    private static final JedisPool jedisPool;

    static {
        // 配置连接池
        JedisPoolConfig poolConfig = new JedisPoolConfig();
        poolConfig.setMaxTotal(8); // 最大连接数
        poolConfig.setMaxIdle(8);  // 最大空闲连接数
        poolConfig.setMinIdle(0);  // 最小空闲连接数
        poolConfig.setMaxWait(Duration.ofMillis(1000)); // 最大等待时间，单位毫秒
        // 创建连接池对象
        jedisPool = new JedisPool(poolConfig, "192.168.100.128",
                6379, 1000, "0924");
    }

    public static Jedis getJedis(){
        return jedisPool.getResource();
    }
}
```
2. 使用JedisConnectionFactory获取Jedis对象  
3. 使用Jedis对象执行redis命令(指令同Redis指令)    

### 1.2.2 SpringDataRedis  
[SpringDataRedis官网](https://spring.io/projects/spring-data-redis)

API:  
工具类：RedisTemplate  
不同数据结构：  
- String: opsForValue()
- Hash: opsForHash()
- List: opsForList()
- Set: opsForSet()
- SortedSet: opsForZSet()  
****

StringRedisTemplate  
需要自己手动处理序列化和反序列化  
序列化工具可以使用 fastjson, objectMapper等  

# 二、项目开发  

<font color="lightblue">新工具</font>:  
Mybatis-plus/Mybatis-flex: Mybatis增强工具
类转换工具: BeanUtils(对于属性名不同使用注解<font color="yellow">@Aliass</font>), MapStruct(需要定义接口，编译时生成实现类)
****

<font color="lightblue">基于redis实现共享Session登录</font>:  
为何使用redis: session存在多台Tomcat不共享session空间，请求切换到不同Tomcat服务会导致数据丢失  
1. 发送短信验证码
2. 短信验证码登录、注册
3. 校验登陆状态  

刷新token的TTL可以专门用一个拦截器进行刷新，该拦截器应当在登录拦截器之前  
****

<font  color="lightblue">缓存</font>:  
缓存是数据交换的缓冲区，存储数据的临时地方，读写快  
通常使用redis作为缓存中间件  
缓存更新策略:  
- 内存淘汰策略  
  不需要自己更新缓存，redis会根据内存淘汰策略自动更新缓存，但是<fonr color="red">一致性差</font>  
- 超时剔除  
  给缓存添加TTL，过期自动删除，一致性一般  
- 主动更新
  编写业务逻辑，在修改数据库的同时更新缓存，<font color="red">一致性好</font>，但是代码复杂，维护成本高
- 业务场景：根据一致性需求来选择不同的方法  

主动更新操作：  
1. 删除缓存：更新数据库时让缓存失效，查询时再更新缓存  ‘
2. 保证操作的同时性：
    - 单体系统：事务  
    - 分布式系统：TTC等分布式事务方案  
3. 操作顺序  
    - 先更新数据库，再删除缓存(√)  
    - 先删除缓存，再更新数据库
****

<font color="lightblue">缓存穿透</font>:  
缓存穿透是指查询一个不存在的数据，由于缓存和数据库都没有该数据，导致每次请求都要查询数据库，造成数据库压力过大甚至宕机  
解决方案:  
1. 使用[布隆过滤器](https://blog.csdn.net/qq_41125219/article/details/119982158)(推荐)：
   将所有可能存在的数据都存入布隆过滤器中，查询时先查询布隆过滤器，如果不存在则直接返回，如果存在则查询缓存和数据库  
2. 缓存空对象：将不存在的数据也缓存起来，设置较短的TTL，防止缓存被频繁查询  

其他方案：  
- 增加id复杂度  
- 做好数据基础格式校验  
- 加强用户权限校验  
- 做好热点参数限流  
****

<font color="lightblue">缓存雪崩</font>:  
缓存雪崩是指缓存大量key同时过期或者redis服务宕机，导致大量请求直接打到数据库，造成数据库压力过大甚至宕机  
解决方案:  
1. 设置不同key的TTL，避免大量key同时过期
2. 利用Redis集群提高服务的可用性
3. 给缓存业务添加降级限流策略  
4. 给业务添加多级缓存
****

<font color="lightblue">缓存击穿</font>:  
缓存击穿也叫热点Key问题，指一个被该并发访问并且缓存重建业务较复杂的key突然失效了，无数的请求访问会在瞬间给数据库带来巨大的冲击  
解决方案:  
1. 使用互斥锁(分布式锁)：在缓存失效时，只有第一个请求能获取到锁，其他请求等待锁释放后再去查询缓存  
2. 逻辑过期：在缓存中存储数据的同时存储一个逻辑过期时间，数据过期后不立即删除，而是继续返回旧数据，
   同时开启一个<font color="red">异步线程</font>去更新缓存  

优缺点：

|  方案  | 优点                                   | 缺点                                 |
|:----:|:-------------------------------------|:----------------------------|
| 互斥锁  | ·无额外内存消耗<br> ·保证数据的一致性<br> ·实现简单<br> | ·线程需要等待，性能受影响<br> ·可能有死锁           |
| 逻辑过期 | 线程无需等待        | ·不保证一致性<br> ·有额外内存消耗<br> ·实现复杂<br> |
****

<font color="lightblue">全局ID生成器</font>:  
特性：唯一性、递增性、安全性、高可用、高性能  
常见方案：
- UUID: 唯一性好，递增性差，长度长，不适合做数据库主键
- 数据库自增: 唯一性好，递增性好，性能差，单点故障
- Redis自增: 唯一性好，递增性好，性能好，需要维护Redis服务
- [雪花算法(Snowflake)](https://blog.csdn.net/weixin_43024834/article/details/135039159): 唯一性好，递增性好，性能好，高可用，复杂度高  
****  

<font color="lightblue">乐观锁</font>:  
悲观锁：认为线程安全问题一定会发生，操作数据前需要获取锁。如Synchronized、Lock  
乐观锁：认为线程安全问题不会发生，操作数据前不获取锁，操作数据时检查数据是否被修改。  
乐观锁常用方式：版本号、时间戳、[CAS](https://blog.csdn.net/caisongcheng_good/article/details/79916873)  
对于synchronized，在单机的情况下可以使用，对于分布式系统需要使用分布式锁
****

<font color="lightblue">分布式锁</font>:  
分布式锁：满足分布式系统或集群模式下多进程可见且互斥的锁  
特性：互斥、多进程可见、高可用、高性能、安全性  
常见的分布式锁实现有Mysql, Redis, Zookeeper等  

| 方案  |     MySQL      |    Redis     | [Zookeeper](https://zookeeper.apache.org/) |
|:---:|:--------------:|:------------:|:------------------------------------------:|
| 互斥  | 利用mysql本身的互斥机制 |  setnx等互斥命令  |              利用节点的唯一性和有序性实现互斥              |
| 高可用 |       好        |      好       |                     好                      |
| 高性能 |       一般       |      好       |                     一般                     |
| 安全性 |   断开连接，自动释放锁   | 利用锁超时时间，到期释放 |               临时节点，断开链接自动释放                |

[Lua编程](https://lua.ac.cn/docs.html)：Lua脚本可以解决释放锁的原子性  
****

[spring事务不生效场景](https://blog.csdn.net/hanjiaqian/article/details/120501741):  
- 访问权限：必须为public修饰  
- 类修饰：类不能为final修饰，方法不能为final修饰  
- <font color="RED">方法调用</font>：同类内部方法调用事务不生效，必须通过代理对象调用  
  可以利用AopContent类来进行代理  
- 未添加注解以注入ioc(@Service, @Component)  
- 多线程调用  
- 数据库引擎可能不支持(MyISAM就不支持事务)  
- spring未开启事务
- 事务传播行为(默认REQUIRED)  
- try-catch捕获异常且未抛出异常，事务不会回滚  
- 异常不匹配或者自定义了回滚异常  

在spring中为了支持编程式事务，专门提供了一个类：<font color="GREEN">TransactionTemplate</font>，在它的execute方法中，就实现了事务的功能。  
****

<font color="lightblue">[Redisson](https://github.com/redisson/redisson)</font>:  
可重入：利用hash结构记录线程id和重入次数  
可重试：利用信号量和pub/sub功能实现等待、唤醒，获取锁失败的重试机制  
超时续约：利用watchDog，每隔一段时间(releaseTime / 3)，重置超时时间  
****

<font color="lightblue">阻塞队列/消息队列</font>:  
阻塞队列：BlockingQueue  
<font color="YELLOW">@PostConstruct</font>: 在类初始化后执行注解的方法  
阻塞队列异步会出现的问题：内存限制、数据安全  
为解决阻塞队列异步出现的问题采用消息队列  
消息队列(Message Queue)：存放消息的队列，消息生产者将消息发送给消息队列，消息消费者从消息队列中获取消息，并消费消息。   
消息队列的实现方式：  
- ActiveMQ
- [RabbitMQ](https://www.rabbitmq.com/docs)
- Kafka
- [RocketMQ](https://rocketmq.apache.org/)

[消息队列笔记](https://blog.csdn.net/qq_45173404/article/details/121687489)  
Redis实现消息队列:  
list结构: BLPUSH, BRPOP  
PubSub: SUBSCRIBE, PUBLISH, PSUBSCRIBE  
Stream(新的数据类型): XADD, XREAD  
Stream类型消息队列Xread命令特点：  
- 消息可回溯  
- 一个消息可以被多个消费者读取  
- 可以阻塞读取
- 有<font color="RED">消息漏读</font>风险  

消费者组：  
- 创建消费者组：`XGROUP CREATE key groupName ID [MKSTREAM]`  
- 添加消费者：`XGROUP CREATECONSUMER key groupName consumerName`  
- 删除消费者：`XGROUP DELCONSUMER key groupName consumerName`  
- 删除消费者组：`XGROUP DESTROY key groupName`  
****  

<font color="lightblue">Feed模式</font>:  
常见模式：Timeline模式(朋友圈)、智能排序(推荐系统)  
实现方案：拉模式(基本不使用)、推模式(用户量少，无大V)、推拉结合(过千万的用户量，有大V)  
****

<font color="lightblue">GEO数据结构</font>:  
GEOADD、GEODIST、GEOHASH、GEOPOS、GEOSEARCH、GEOSEARCHSTORE
****

<font color="lightblue">BitMap</font>:  
SETBIT、GETBIT、BITCOUNT、BITFIELD、BITFIELF_RO、BITOP、BITOPS  

[HyperLogLog](https://blog.csdn.net/2301_82241859/article/details/137119275): PFADD、PFCOUNT、PFMERGE  
****

<font color="lightblue">Redis持久化</font>:  
<font color="RED">RDB持久化</font>:   
Redis默认持久化方式，保存为RDB文件，保存文件为dump.rdb  
bgsave开始时会fork得到子进程，共享主进程内存数据，完成fork后读取内存数据写入RDB  
防止读写冲突：copy-on-write  
- 主进程读操作，访问共享内存  
- 主进程写操作，会拷贝一份数据，在新拷贝的数据空间写入数据，此时共享内存页表会发生变化  

<font color="RED">AOF持久化</font>:  
AOF持久化方式，保存为AOF文件，保存文件为appendonly.aof  
刷盘策略：addpenfsync always/everysec/no  
两者的对比：  

|       |    RDB    |     AOF      |
|:-----:|:---------:|:------------:|
| 持久化方式 | 对整个内存做快照  |  记录每次执行的命令   |
| 数据完整性 | 两次备份之间会丢失 | 相对完整，取决于刷盘策略 |
|文件大小|小|大|
|恢复速度|快|慢|
|数据恢复优先级|低|高|
|系统资源占有|大量CPU和内存消耗|主要占用磁盘IO资源，重写才会占用大量CPU和内存|
|场景|容忍数分钟数据丢失，追求更快的启动方式|对数据安全性要求较高|
****

<font color="lightblue">主从集群</font>:  
开启主从关系：  
```  bash  
slaveof  <masterip> <masterport>  (不建议)
replicaof <masterip> <masterport>
```
查看：`INFO REPLICATION`
****

<font color="lightblue">数据同步原理</font>:  
主从第一次同步时全量同步(使用的是RDB)  
如何判断是不是第一次同步数据：  
- replication id：数据集标记，id一致表示同一数据集。每个master有唯一的replid，slave会继承主的replid
- offset：数据集偏移量，slave的offset小于master的offset, 表示slave数据需要更新  

不是第一次采用增量同步(repl_baklog中取offset后的数据)  
<font color="RED">注意</font>: repl_baklog大小有上限，写满后会覆盖最早的数据，若是slave断开太久，导致数据
被覆盖，此时只能使用<font color="RED">全量同步</font>  
数据同步优化：  
- 在master中配置repl-diskless-sync yes启用无磁盘复制，直接发送到网络中  
- Redis单节点上的内存占用不要太大，减少RDB导致的过多磁盘IO  
- 适当提高repl_backlog大小,发现slave宕机尽快实现故障恢复  
- 限制一个master上的slave节点数量，若slave太多采用主-从-从链式结构  
****

<font color="lightblue">哨兵机制</font>:  
哨兵机制作用： 
- 监控：Sentinel会不断检查master和slave是否按预期工作  
- 自动故障恢复：当master挂掉时，Sentinel会自动将一个slave提升为master，当故障实例恢复后也以新的master为主节点  
- 通知：Sentinel充当Redis客户端的服务发现来源，当集群发生故障转移时会将最新信息推送给Redis客户端  

监控机制：基于心跳机制检测服务状态，每隔1秒像集群每个实例发送PING命令  
- 主观下线：当实例未在规定时间内响应  
- 客观下线：超过指定数量(quorum)的Sentinel都认为该实例主管下线，则该实例客观下线，quorum一般为N/2+1，其中N为Sentinel数量  

选举新的master：  
- 判断slave与master断开时间长短，超过指定值(down-after-milliseconds * 10)则会排除该slave节点
- 判断slave-priority值，值越小优先级越高，为0永不参与选举
- slave-priority值相同判断slave的offset，越大说明越新，优先级越高
- 最后判断slave运行id大小

如何实现按故障转移：  
- Sentinel会向选中的slave发送slaveof no one
- Sentinel会向其他slave发送slaveof \<newMasterIp> \<newMasterPort>
- 将故障节点标记为slave

RedisTemplate配置读写分离：  
- 先要在配置文件配置哨兵  
- 实现类：configurationBuilderCustomizer
- ReadForm: MASTER, MASTER_PREFERRED, REPLICA, REPLICA_PREFERRED(这个优先)  

****

<font color="lightblue">分片集群</font>:  
特征：  
- 多个master,每个master保存不同数据  
- 每个master有多个slave节点
- master之间通过ping检测彼此健康状态
- 客户端可以访问集群任意节点，最终都会转发到正确节点

[散列插槽](https://blog.csdn.net/qq_41587243/article/details/115331897)  
集群伸缩、故障转移  
****

<font color="lightblue">JVM进程缓存</font>:  
[caffeine](https://github.com/ben-manes/caffeine)  
三种驱逐策略：基于时间、基于容量、基于引用(过期不是立马清除)  
实现方式：实现配置类CaffeineConfig并在里面设置Bean对象  
****

<font color="lightblue">Lua语法入门</font>:  
数据类型：nil、boolean、number、string、table、function  
函数：  
``` lua
function 函数名(arg1, arg2...)
    -- 函数体
    return 返回值
end
```
条件控制：and or not  
``` lua
if 条件 then
  -- 条件为真执行
else 
  -- 条件为假执行
end
```
****

<font color="lightblue">多级缓存</font>:  
[OpenResty](https://openresty.org/cn/)  
openResty获取请求参数：
- Get请求参数(?id=1001) `local args = ngx.req.get_uri_args()`
- Post请求参数(id=1001)
  ``` lua 
  ngx.req.read_body()
  local args = ngx.req.get_post_args()
  ```
- JSON参数({"id": 1001})
  ``` lua
  ngx.req.read_body()
  local args = ngx.req.get_body_data()
  ```
- 请求头 `local headers = ngx.req.get_headers()`
- 路径占位符
  ``` lua
  location ~ /item/(\d+) {
      content_by_lua_file lua/item.lua;
  }
  ```

Tomcat负载均衡：
``` 
upstream tomcat-cluster {
    hash $request_uri;
    server 192.168.100.1:8081;
    server 192.168.100.1:8082;
}
server {
    location /item {
        proxy_pass http://tomcat-cluster;
    }
}
```
冷启动：服务刚启动时，redis没有缓存，所有商品第一次查询时添加缓存会给数据库带来较大压力  
缓存预热：利用大数据统计用户访问的热点数据，项目启动时将这些热点数据提前查询并缓存到Redis中

OpenResty中的Redis模块：
- 导入Redis模块：
    ``` lua
    local redis = require("resty.redis")
    local red = redis:new()
    red:set_timeout(1000, 1000, 1000)
    ```  
- 释放redis连接Api:
    ``` lua
    -- 关闭redis连接的工具方法，其实是放入连接池
    local function close_redis(red)
        local pool_max_idle_time = 10000 -- 连接的空闲时间，单位是毫秒
        local pool_size = 100 --连接池大小
        local ok, err = red:set_keepalive(pool_max_idle_time, pool_size)
        if not ok then
            ngx.log(ngx.ERR, "放入redis连接池失败: ", err)
        end
    end
    ```
- 读取redis数据：
    ``` lua
    -- 查询redis的方法 ip和port是redis地址，key是查询的key
    local function read_redis(ip, port, key)
        -- 获取一个连接
        local ok, err = red:connect(ip, port)
        if not ok then
            ngx.log(ngx.ERR, "连接redis失败 : ", err)
            return nil
        end
        -- 查询redis
        local resp, err = red:get(key)
        -- 查询失败处理
        if not resp then
            ngx.log(ngx.ERR, "查询Redis失败: ", err, ", key = " , key)
        end
        --得到的数据为空处理
        if resp == ngx.null then
            resp = nil
            ngx.log(ngx.ERR, "查询Redis数据为空, key = ", key)
        end
        close_redis(red)
        return resp
    end
    ```

OpenResty本地缓存：
``` lua
-- 开启共享字典
lua_shared_dict item_cache 1500m;
-- 操作共享字典  
local item_cache = ngx.shared.item_cache;
item_cache:set('key', 'value', 1000);
local val = item_cache:get('key');
```

多级缓存：浏览器客户端缓存 -> OpenResty本地缓存 -> Redis缓存 -> 进程缓存 -> 数据库
****

<font color="lightblue">缓存同步策略</font>:  
- 设置有效期：给缓存设置有效期，到期后自动删除
- 同步双写：修改数据库时直接修改缓存  
- 异步通知：当数据库发生变化时，相关服务监听到通知后修改缓存数据  

[Spring Cache的使用](explanation/SpringCache.md): 基于注解的缓存功能

[Canal](https://github.com/alibaba/canal): 主要用途是基于 MySQL 数据库增量日志解析，提供增量数据订阅和消费  
<font color="yellow">@CanalTable("table_name")</font>表示监听的表  
实体与数据库映射：
- <font color="yellow">@Id</font>: 表示表的id字段
- <font color="yellow">@Column(name = "name")</font>: 表示字段名不同
- <font color="yellow">@Transient</font>: 表示该字段不是监听的表的字段
****

<font color="lightblue">Redis实战经验</font>:  
key结构：[业务名称]:[数据名]:[id]  
key底层编码包含int, embstr, raw, 长度小于44字节使用embstr，是连续存储，内存占用少  
BigKey: 根据Key的大小和成员数量综合判定  
BigKey危害: 网络阻塞、数据倾斜、Redis阻塞、CPU压力  
如何发现BigKey: redis-cli --bigkeys, scan命令, 第三方工具(Redis-Rdb-Tools), 网络监控  
调整hash的entry上限：修改hash-max-ziplist-entries  
单机批处理：原生M操作、Pipline  
集群下批处理：串行命令、串行slot、并行slot(推荐且springboot已经实现，stringRedisTemplate)、hash_tag(当在key前加上{xxx}会默认都适用xxx来分配slot)  
持久化配置：  
- 用来做缓存的Redis实例尽量不开启持久化
- 建议关闭RDB，使用AOF持久化  
- 利用脚本定期在slave节点做RDB，实现数据备份
- 设置合理rewrite阈值，避免频繁的bgrewrite  
- 配置no-appendfsync-on-rewrite=yes，禁止rewrite期间做aof  

慢查询：  
- slowlog-log-slower-than: 1000
- slowlog-max-len: 128
- 配置：config set slowlog-log-slower-than 1000

查看内存信息：info memory, memory xxx
****

# 三、Redis原理篇
<font color="lightblue">数据结构</font>:  
**动态字符串SDS:**  
- 8/16/32/64
- 内存预分配：(n < 1M) 2*n+1; (n > 1M) n + 1M + 1, n为扩展后字符串长度  

**IntSet:**  
- encoding: 16/32/64位 
- Redis确保IntSet的元素唯一且有序
- 具备升级类型，节省内存
- 可变使用二分查找查询

**Dict:**  
- 三部分：哈希表、哈希节点、字典
- rehash（扩容/收缩操作）
  - 负载因子：LoadFactor(α) = used / size
  - 扩容时机：α>=1且未执行BGSAVE和BGREWRITEAOF等后台进程；α>5直接强制执行
  - 缩容时机：α<0.1且大小大于4
  - 哈希表初始化大小为4
- 每个都有两个hash表，另一个rehash的时候使用
- 渐进式扩容：增删查改时都将一个链上的数据rehash
- rehash的时候ht[0]只减不增，新增的时候只在h[1]里面操作，其他操作需要两个表进行查找，h[0]和h[1]数据不会重复  

**ZipList:**  
- 组成：zlbytes(4字节,表示总字节数), zltail(4字节, 尾节点与起始地址之间的字节数), 
  zllen(2字节, entry个数), entry... ,zlend(1字节, 表示结束符0xff)
- entry: previous_entry_length(1/5字节, 表示前一个entry的长度, 0xfe表示长度为5字节,后面四个字节为真实数据长度), 
  encoding(1/2/5字节, 记录content数据类型和长度, 00/01/10表示字符串), content(内容)
- encoding以11开头表示整数，encoding固定1字节
  - 1111xxxx: xxxx位置保存数值，0001~1101(0 - 12)， 减1为实际值
  - 11000000: int16_t(2bytes)
  - 11010000: int32_t(4bytes)
  - 11100000: int64_t(8bytes)
  - 11110000: 24位有符整数(3bytes)
  - 11111110: 8位有符整数(1bytes)
- 存储长度的数值(zlbytes, zltail, zllen)采用<font color="RED">小端存储</font>(低位存储在低地址)
- 缺陷：entry个数限制；连锁更新
- Redis7.0之后弃用，使用listpack

**ListPack:**  
- 组成：\<tot-bytes>\<num-entrys><entry...>\<listpack-end-byte>
- Entry: \<entry-encoding>\<entry-data>\<entry-tot-len>
- entry-tot-len不包括自己的长度，只包含encoding和data的长度，
  且每个byte最高位(0表示结束，1表示为结束)，剩下7bits采用<font color="RED">大端存储</font>

**QuickList:**  
- 双端链表，节点为ZipList, Redis7.0之后改为listpack

**SkipList:**  
- 链表结构，元素升序排列存储
- 节点可能包含多个指针，指针跨度不同
- 节点按照score值排序
- 节点组成：ele(节点存储的值), score, \*backward, level(里面包含*forward, span)[]

**RedisObject:**  
- Redis任意数据类型的键值均会封装为一个RedisObject
- 源码：
  ``` 
  #define OBJ_STRING 0
  #define OBJ_LIST 1
  #define OBJ_SET 2
  #define OBJ_ZSET 3
  #define OBJ_HASH 4
  
  typedef struct redisObject { 
    unsigned type: 4;  // 对象类型, 4bit
    unsigned encoding: 4;  // 底层编码方式, 4bit
    unsigned lru: LRU_BITS;  // LRU_BITS为24bit，内存回收的时候使用
                             // LRU以秒为单位记录最近访问时间
                             // LFU前16位以分钟为单位记录最近一次访问时间，低8位记录逻辑访问次数  
    int refcount;  // 对象引用计数器
    void *ptr;  // 指向实际数据的空间
  } robj
  ```
- 编码方式：
  - OBJ_ENCODING_RAW: raw编码动态字符串
  - OBJ_ENCODING_INT: long类型整数编码
  - OBJ_ENCODING_HT: dict字典编码/hash表
  - OBJ_ENCODING_ZIPLIST: 压缩列表
  - OBJ_ENCODING_INTSET: 整数集合
  - OBJ_ENCODING_SKIPLIST: 跳表
  - OBJ_ENCODING_QUICKLIST: 快速列表
  - OBJ_ENCODING_EMBSTR: embstr字符串编码
  - OBJ_ENCODING_LINKEDLIST: 双端链表
  - OBJ_ENCODING_STREAM: stream流
- 类型可用编码：
  - String: Raw, Embstr(不超过44字节), Int
  - List: QuickList
  - Set: IntSet, HT
  - ZSet: SkipList + HT, 元素少且小会使用ZipList(7.0之后为listpack)
    - 使用ZipList条件: 元素小于64字节，元素个数小于128
  - Hash: HT, 元素少且小会使用ZipList(7.0之后为listpack)
    - 使用ZipList条件: 元素小于64字节，元素个数小于512
****

<font color="lightblue">网络模型</font>:  
**用户空间和内核空间:**  
- 用户空间: 用户进程，用户态，用户态的进程运行在用户空间，用户空间可以访问用户态的内存，不能访问内核空间
- 内核空间: 内核进程，内核态，内核态的进程运行在内核空间
- 线程切换: 用户态线程切换内核态线程，内核态线程切换用户态线程

**五种IO模型：**  
- 阻塞IO
- 非阻塞IO(轮询空转)
- [IO多路复用](https://zhuanlan.zhihu.com/p/367591714)
- 信号驱动IO
- 异步IO

<font color="PINK">Q: Redis是单线程么？</font>  
A: 核心业务(命令处理)未单线程，整个Redis为单线程，v6.0之后核心网络模型中引入了多线程  

<font color="PINK">Q: 为何Redis要坚持单线程？</font>  
- 线程切换开销大
- 纯内存操作，速度本身就很快，多线程对性能影响不大 
- 多线程面临线程安全问题，需要引入线程锁，复杂度增高

Redis网络模型:  
- 解析客户端命令和写响应结果采用多线程，核心的命令执行和IO多路复用模块依然由主线程执行  

****

<font color="lightblue">通信协议</font>:  
- +: 单行字符开头, CRLF(\r\n)结尾
- $: 多行字符开头
- *：数组，并跟上数字，数字表示数组元素个数，后续跟上元素
- \-：字符串异常信息
- :开头：数字格式字符串

****

<font color="lightblue">内存策略</font>:  
- 底层使用dict存储 key-value 以及 key-ttl
- 过期策略
  - 方式：惰性删除(访问key时检查ttl，过期就删除)、周期删除(周期性抽取部分过期的key, 然后执行删除)
  - 周期删除有FAST(beforeSleep时执行)和SLOW(initServer设置定期任务)两种模式
- 淘汰策略
  - 任何命令执行前都会检查内存使用情况
  - 方式：LRU、LFU、TTL、Random、noeviction
****

<font color="lightblue"></font>:  
<font color="lightblue"></font>:  
<font color="lightblue"></font>:  
<font color="lightblue"></font>:  




















