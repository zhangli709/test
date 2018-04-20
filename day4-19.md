
## redis
# 五大类型 string hash list set zset

1. type  查看类型  key * 查看所有key
2. string   set / get  设置，获取
* 增 set p 2     mset/msetnx 批量赋值 / mget   incr/decr 依次递增/递减    incrby / decrby 递增/递减指定值   
*    incrbyfloat  增加小数。  append  （追加， 5 追加5 为55）   getrange m 0 -1 两边闭区间。
* 删 del p 
* 改
* 查
* strlen key 返回长度
* setex key seconds value 设置过期时间
3. hash  放用户信息  h
*  hset / hget   hgetall 拿所有，fields  values
*  hvals xiaoshuo   获取val  hkeys xiaohuo 获取key
*  hdel xiaoshuo name 删除。
4. list 双向列表   push
* lpush key value1 value2 左插入
* rpush key  value1 value2 右插入  设置值
* linsert key before / after pivot val
* lrange 取出指定范围内的值。
* lpop / rpop 删除左/右边第一个
* llen 获取长度。
* lrem key count value 移除列表元素
* rpushx key value为已存在的列表添加值。
5. set 集合   add
* 增 sadd  添加一个或多个
* 删 spop 无序的删除
* 改 
* 查 smembers 
* scard 查个数
* sdiff key1 key2 返回差集
* sinter key1 key2 返回子集
6. zset 有序集合 相比多了一项分数  zadd
* 增 zadd g 分数 key
* 删 zrem key 删除  zremrangebylex key min max 移除指定区间的成员
* 改 
* 查 zscore g m1     
* 排序 zrange g 0 -1   反向 zrevrange 
* zcard key 获取成员数

## 扩展 爬虫
# 获取页面源码

1. requests
2. beautifulsoup bs4
* BS4本身是一种对描述语言进行封装的函数操作模块，通过提供面向对象的操作方式将文档对象中的各种节点、标签、属性、内容等等
* 都封装成了python中对象的属性，在查询操作过程中，通过调用指定的函数直接进行数据 匹配检索操作，非常的简单非常的灵活。
* 一般BS4将HTML文档对象会转换成如下四种类型组合的文档树

* Tag：标签对象
* NavigableString：字符内容操作对象
* BeautifulSoup：文档对象
* Comment：特殊类型的NavigableString

*
* 
*
*
3. scrapy 


## 实战项目
# 登录 redis + mysql
1. pip install redis 安装redis
2. 链接mysql
3. 链接redis
* import redis
* redis.Redis()
4.获取姓名密码参数 
* python xxx.py argv1 argv2
* import sys
* sys.argv[1]
5. 访问redis, 判断你输入的姓名和密码和redis中保存的用户名，密码是否正确
6. 和redis不匹配，则查询mysql, select 操作，
7. mysql 有查询结果的话， 则更新到redis中，否则就没有该用户。


## Django
# Web框架，开放源代码应用，由python写成。遵守BSD版权，
# 采用MVC设计模式，即模型M 视图V 控制器C
