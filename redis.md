# redis

1. 概念
2. 下载安装
3. 命令操作
   1. 数据结构
4. 持久化操作
5. 使用Java客户端操作redis

redis

概念:redis是一款高性能的NOSQL系列的菲关系型数据库

文件介绍

redis.windows.conf 配置文件

redis-cli.exe 客户端

redis-server.exe 服务器端

redis数据结构 key,value 其中键都是字符串 value有5中数据结构

- 字符串 String
- 哈希类型 hash
- 列表类型 list
- 集合类型 set有序集合类型 sortedset

### **命令操作**

- 字符串
  - 存储:set key value
  - 获取:get key
  - 删除:del key
- 哈希类型
  - 存储:hset key field value
  - 获取:hget key field
  - 删除:hdel key field
  - 获取所有的键值对 hgetall key
- 列表类型
  - 存储:
    - lpush key value:从列表左边加入
      rpush key value:从列表右边加入
  - 获取:
    - lrange key start end :范围获取
  - 删除:
    - lpop key: 从列表左边删除最左边的元素并将元素返回
    - rpop key: 从列表左边删除最右边的元素并将元素返回
- 集合类型
  - 存储:sadd key value
  - 获取:smenbers key:获取所有元素
  - 删除:srem key value
- 有序集合
  - 存储:zadd keyscore value
  - 获取:zrange key start end
  - 删除:zren key value
- 通用命令
- keys * 查询所有
- type name 查看类型
- del key 删除指定的key

### 持久化

redis是一个内存数据库,当redis服务器重启,数据会丢失,我们可以持久化

1. redis持久化机制

   1. RDB:默认方式,不需要配置

      在一定的间时间中,检测key的变化情况,然后持久化数据

      1. 编辑配置文件

         save 900 1

         save 300 10

         save 60  10000

   2. AOF:日志记录的方式,可以记录每一条命令的操作.只要以改变就修改

      1. 编辑配置文件 

### Java客户端 Jedis

Jedis:一款java操作redis数据库的工具

使用步骤:

1. 下载jedis的jar包
2. 使用

jedis连接池 Jedispool

​	使用

创建JedisPool连接池对象

调用方法 getResource()方法