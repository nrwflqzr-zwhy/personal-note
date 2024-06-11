# 二、Redis 概述安装

-   Redis是一个开源的 key-value 存储系统
-   和 Memcached 类似，它支持存储的 value 类型相对更多，包括 string(字符串)、list(链表)、set(集合)、zset(sorted set --有序集合)和 hash（哈希类型）
-   这些数据类型都支持 push/pop、add/remove 及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的
-   在此基础上，Redis支持各种不同方式的排序
-   与memcached一样，为了保证效率，数据都是缓存在内存中
-   区别的是Redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件
-   并且在此基础上实现了master-slave(主从)同步

## 2.1 应用场景

### 2.1.1 配合关系型数据库做高速缓存

-   高频次，热门访问的数据，降低数据库 IO
-   分布式架构，做 session 共享

<img src="Redis.images/image-20240607152333964.png" alt="image-20240607152333964" style="zoom:50%;" />

### 2.1.2 多样的数据结构存储持久化数据

<img src="Redis.images/image-20240607152357155.png" alt="image-20240607152357155" style="zoom:50%;" />

## 2.2 Redis 安装

### 2.2.1 安装目录 /usr/local/bin

-   redis-benchmark:性能测试工具
-   redis-check-aof：修复有问题的AOF文件
-   redis-check-dump：修复有问题的dump.rdb文件
-   redis-sentinel：Redis集群使用
-   redis-server：Redis服务器启动命令
-   redis-cli：客户端，操作入口

### 2.2.2 前台启动

<img src="Redis.images/image-20240607153510369.png" alt="image-20240607153510369" style="zoom:67%;" />

```shell
redis-server # 命令行窗口不能关闭，否则服务器停止
```

### 2.2.3 后台启动

#### 2.2.3.1 备份 redis.conf

拷贝一份 redis.conf 

```shell
cp /opt/redis-3.2.5/redis.conf /myredis
```

#### 2.2.5.2 修改后台启动设置 

128: daemonize no 改成 yes，让服务在后台启动

#### 2.2.5.3 Redis 启动

```shell
redis-server /myredis/redis.conf
ps -ef | grep redis
```

#### 2.2.5.4 客户端访问

```shell
redis-cli
```

#### 2.2.5.5 Redis 关闭

```shell
redis-cli shutdown
也可进入终端再关闭
```

### 2.2.4 Redis 相关知识

-   端口 6379
-   默认存在16个数据库，下标从0开始，初始默认使用0号库；使用命令 select \<dbid> 来切换数据库: select 8
-   所有库使用同样的密码
-   dbsize 查看当前数据库的 key 的数量
-   flushdb 清空当前库；flushall 通杀全部库

Redis是**单线程+多路IO复用技术**

多路复用是指使用一个线程来检查多个文件描述符（Socket）的就绪状态，比如调用select和poll函数，传入多个文件描述符，如果有一个文件描述符就绪，则返回，否则阻塞直到超时。得到就绪状态后真正的操作可以在同一个线程里执行，也可以启动线程执行（比如使用线程池）

串行  vs  多线程+锁（memcached） vs  单线程+多路IO复用(Redis)

（与Memcache三点不同: 支持多数据类型，支持持久化，单线程+多路IO复用）

# 三、常用五大数据类型

## 3.1 Redis 键(key)

```shell
key * # 查看当前库所有key
exists key # 判断某个key是否存在
type key # 查看你的key是什么类型
del key # 删除指定的key数据
unlink key # 根据value选择非阻塞删除
	仅将keys从keyspace元数据中删除，真正的删除会在后续异步操作。
expire key 10 # 10秒钟：为给定的key设置过期时间
ttl key # 查看还有多少秒过期，-1表示永不过期，-2表示已过期
select # 命令切换数据库
dbsize # 查看当前数据库的key的数量
flushdb # 清空当前库
flushall # 通杀全部库
```

## 3.2 Redis 字符串（String）

### 3.2.1 简介

-   String类型是**二进制安全**的。意味着Redis的String可以包含任何数据。比如jpg图片或者序列化的对象。
-   String类型是Redis最基本的数据类型，一个Redis中字符串value最多可以是512M

### 3.2.2 常用命令

````shell
set <key> <value> # 添加键值对
```
*NX：当数据库中key不存在时，可以将key-value添加数据库
*XX：当数据库中key存在时，可以将key-value添加数据库，与NX参数互斥
*EX：key的超时秒数
*PX：key的超时毫秒数，与EX互斥
*表示非必选
```
````

```shell
get <key> # 查询对应键值
append <key> <value> # 将给定的<value>追加到原值的末尾，字符串拼接
strlen <key> # 获得值的长度
setnx <key> <value> # 只有在 key 不存在时，设置 key 的值

incr  <key>
	# 将 key 中储存的数字值增1
	# 只能对数字值操作，如果为空，新增值为1
decr  <key>
	# 将 key 中储存的数字值减1
	# 只能对数字值操作，如果为空，新增值为-1
incrby / decrby <key><strip> # 将 key 中储存的数字值增减。自定义步长。
```

```shell
mset <key1> <value1> <key2> <value2> # 同时设置一个或多个 key-value对  
mget <key1> <key2> <key3> # 同时获取一个或多个 value  
msetnx <key1> <value1> <key2> <value2> # 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。原子性，有一个失败则都失败
```

```shell
getrange <key> <起始位置> <结束位置> # 获得值的范围，类似java中的substring，前包，后包
setrange <key> <起始位置> <value> # 用 <value> 覆写<key>所储存的字符串值，从<起始位置>开始(索引从0开始)。
setex <key> <过期时间> <value> # 设置键值的同时，设置过期时间，单位秒。
getset <key> <value> # 以新换旧，设置了新值同时获得旧值。
```

### 3.2.3 数据结构

String 的数据结构为**简单动态字符串**(Simple Dynamic String,缩写SDS)。是可以修改的字符串，内部结构实现上类似于 Java 的 ArrayList，采用预分配冗余空间的方式来减少内存的频繁分配。