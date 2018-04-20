
### mysql

## 安装PyMySQL
> pip install PyMySQL
## 数据库的链接
# _*_ coding:utf-8 _*_
> import pymysql
# 打开数据库链接
> db = pymysql.connect(host='localhost',
>    user='root',
>   password='123456',
>    db='srs',
>    port=3306,
>    charset='utf8')
# 3.获取游标
>cursor = db.cursor()
# 4. 执行sql,提交。
>try:
>    sql = '''update tbcourse set cosname='语文',cosintro='哈哈哈' where cosid=7777;'''
>    cursor.execute(sql)
>    db.commit()
>except:
>    db.rollback()
# 2.关闭链接
>db.close()

### Redis -- REmote Dlctionary Server 
# 简介 
1. 是一个有Salvatore Sanfilippo写的key-value存储系统
2. 它时一个开源的使用ANSI C语言编写 遵守BSD协议 支持网络 可基于内存持久化的日志型 key-value数据库，并提供多张语言的API
3. 通常被称为数据结构服务器，因为值values可以是 String Map list sets sorted sets等类型 

# 特点
1. 支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用
2. 支持key-value list set zset hash等数据结构的存储
3. 支持数据的备份，即master-slave模式的数据备份

# 优势
1. 读 110000次/秒  写81000次/秒
2. 支持二进制的Strings, Lists , Hashes, Sets, Ordered Sets
3. 原子 -- 原子性。
4. 支持 publish / subscribe , 通知 ， key 过期等特性

# 启动
1. redis-server / redis-cli
2. redis-server &

# 添加密码
1. 找到redis.conf,通过查找找到requirepass, 并令requirepass 123456

# 访问指定IP:端口的服务器，redis
1.  redis-cli -h id -p port -a password

## redis的五大类型 string hash list set zset
# string 字符串类型
1. 最基本的数据类型，可以包含任何数据，一个见最大存储512MB
2. 使用set 和 get 命令
3. getrange key start end 两边闭区间
4. getset key value 设置新值，并返回旧值
5. getbit key offset
6. mget key1 key2 同时获得多个key值
7. setbit key offset value 
8. setex key seconds value, 关联值，并且同时设置过期时间
9. setnx key value 只有在key不存在时设置key
10. setrange key offset value 用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。 
11. strlen key 返回key所存储的值的长度
12. mset key value key value   同时设置多个键值对
13. msetnx key value  key value 同时设置多个键值对，当且仅当key之前不存在
14. psetex key milliseconds value 设置过期时间，以毫秒计算
15. incr key 将key中的数字值增一
16. incrby key increment 将key所存储的值加上给定的增量只
17. incrbyfloat key increment 将key所存储的值加上给定的浮点增量值
18. decr keky 将key中存储的数字减一
19. decrby key decrement 将key中的值减去给定的减量值
20. append key value 如果key存在，且为字符串，append将指定的value追加到后面 

# hash 哈希  存储对象
1. hdel key field1 field2  删除一个或多个哈希表字段
2. hexists key field 查看指定的字段是否存在
3. hget key field 获取指定字段的值
4. hgetall key  获取在哈希表中指定key的所有字段和值
5. hincrby key field increment 为哈希表key 指定字段的整数值加上增量increment
6. hincrbyfloat key field increment
7. hkeys key
8. hlen key 
9. hmget key field1 field2
10. hmset key field1 value1  field2 value2
11. hset key field value
12. hsetnx key field value
13. hvals key
14. hscan key cursor [match pattern][coount count]

# 列表
1. blpop key1 key2 timeout
2. brpop key1 key2 timeout
3. brpoplpush source destination timeout 
4. lindex key index 通过索引获取列表中的元素
5. linsert key before/after pivot value 在列表的原色前后者后插入元素
6. lien key 获取列表长度
7. lpop key 移出并获取列表的第一个元素
8. lpush key value1 value2 将一个或多个值插入到列表头部
9. lpushx key value 将一个值插入到已经粗在的列表头部
10. lrange key start stop 获取指定范围内的元素
11. lrem key count value 移除列表元素
12. lset key index value 通过索引设置列表元素的值
13. ltrim key start stop 让列表只保留只当区间内的额元素，删除其余
14. rpop key 移除并获取列表最后一个元素
15. rpoplpush source destination 移除列表的最后一个元素，并将该元素加到另一个列表返回i
16. rpush key value1 values 在列表中添加一个或多个值
17. rpushx key value 为已经存在的列表添加值

# set 集合  无序集合，集合成员是唯一的，集合是通过哈希表实现的，2^32-1

1. sadd key menber1 member2 向集合添加一个或多个成员
2. scard key 获取集合的成员数
3. sdiff key1 key2 返回给定所有集合的差集
4. sdiffstore destination key1 key2 返回给定所有集合的差集并存储在destination中
5. sinter key1 key2 返回给定所有集合的交集
6. sinterstore destination key1 key2 返回给定所有集合的交集并存储在destination中
7. sismember key menber 判断menber 元素是否是集合key的成员
8. smembers key 返回集合的所有成员
9. smove source destination member 将member 元素从source集合移动到destination集合
10. spop key 移除并返回集合中的一个随机元素
11. srandmember key [count] 返回集合中一个或多个随机数
12. srem key member1 member2 移除集合中一个或多个成员
13. sunion key1 key2 返回所有给定集合的并集
14. sunionstore destination key1 key2 所有给定集合并集存储在destination 集合中
15. sscan key cursor [match pattern][count count]迭代集合中的元素

# sorted set 有序集合，相比普通集合，每个元素都会关联一个double类型的分数，通过分数来为集合的成员排序

1. zadd key score1 member1 [score2 member2] 向有序集合添加一个或多个成员，或者更新已经存在的成员的分数。
2. zcard key 获取有序集合的成员数
3. zcount key min max 计算在有序集合中指定区间分数的成员数。
4. zincrby key increment member 有序集合中对指定成员的分数嘉盛增量increment 
5. zinterstore destination numkeys key [key] 计算给定的一个或多个有序集的交集，并将结果存储在i性能的有序集合里
6. zlexcount key min max 在有序结合中计算制定字典区间内成员数量
7. 