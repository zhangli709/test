# Linux Study

## Linux平台安装python3.6.4教程
1. wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
2. tar xf Python-3.6.4 tgz
3. cd Python-3.6.4
4. yum install -y zlib-devel
5. ./configure --prefix=/usr/local/python3
* 如果执行上面这一步时报一个关于C的错误，时由于缺少gcc的库要先安装gcc的库后再执行上面的语句，安装gcc的库：yum install -y gcc
6. make && make install
7. cd /etc/profile.d
8. echo 'export PATH=$PATH:/usr/local/python3/bin/' > python3.sh
9. 执行完毕后logout重新连接一下。

## Linux 
### 通用操作系统
1. 任务：任务调度，内存分配，处理外围设备
2. 组成：内核和系统程序（shell-人机对话的窗口， 设备驱动，底层库，服务程序等）
3. 发展史:由linus Torvalds编写
4. free: 自由而非免费

### 优点
1. 通用的操作系统， 不跟特定的硬件绑定。
2. 95%是C语言编写，有可移植性。
3. 具有内核编程接口
4.  支持多用户和多任务（后期团队一起登录，一起开发）
5. 支持安全的分层文件系统
6. 拥有大量的实用程序
7. 进程间通信
8. 强大的文档

## 命令按钮
### 登录和关机
1. adduser student 添加用户
2. passwd student 添加用户对应的密码
3. shutdown 关机

### 文件管理
1. ls -al　　ls -l/ 查看其他目录中的文件
2. pwd 查看自己所在的目录
3. mkdir / rmdir  创建和删除目录  touch / rm -rf  创建和删除文件
4. cd ../.   返回上一级   当前目录
5. copy / move 复制 和 剪切
6. * 所有
7. uniq / diff / file  去重/对比/查看文档类型
8. find 找文件夹  grep 找内容

### 显示文件内容
* cat | less / more

### 根目录下文件
* root / home / usr / etc /  这是最重要的几个

### 帮助
* man / info / --help  

### 下载文件
1. wget url
2. gzip / gunzip  压缩和解压缩
3. tar -cvf / -xvf  压缩和解压缩
4. xz/ xz -d  压缩和解压缩

### 链接
* ln  oldfile newfile 　　 ln -s

### 包管理工具
* yum / npm
* install
* list
* uptate

##### 系统命令
1. systemctl start / stop / restart / status
2. 防火墙80开洞 　　firewall-cmd --zone=public --add-port=80/tcp --permanent
3. netstat -na | grep 3306 查看自己3306端口是否开启
4. netstat -ntlp 查看当前哪些端口在工作
5. systemctl enable / disable 设置开关机自动启动
6. top 任务管理器  kill -9 进程号   杀进程
7. chmod u+x/644 文件名  给文件加上执行的权限 u/g/o   

### 网络命令
1. ifconfig 　　ip address  查看自己ip
2. ping -s 500 -c 3 www.baidu.com　　s-单次字节　　c-次数　　请求3次，每次给我500字节
3. netstat -nap　　查看端口
4. netstat -nap 2>result.txt　　错误重定向，
5. netstat -nap > result.txt 2>error.txt
6. wireshark / ethereal　　数据窃听，安装此软件，并且把网卡设置为混杂模式
7. ssh root@ip　　从一个阿里云，登录到另一个阿里云
8. sftp root@localhost
9. Upload file 上传文件　　Download file 下载文件

###  ping to death分布式拒绝服务攻击   　　--> 防D 买阿里云的服务
* DDos = Disributed Deny of Service　　ping包   　　——> ping + 网站名
* ms　　延迟 发送请求开始到重新接收到信息的时间。
* TCP flood tcp包

### 配置环境变量
1. 用户登录就执行的东西，写在.bash_profile或者.bashrc中
2. 开机就执行的程序，写在rc.local中。
3. crond 计划任务，时间到了就执行的文件。
* crontab -e 命令来编辑
* 0-59 0-23 1-31 1-12 0-6 command 分钟 小时 天 月 星期 命令

## vim 的使用

###下载配置文件
1. wget + 下载地址 ——下载一个vim的编辑工具，redis.
2.　　.vimrc 新建一个，并在里面配置 set nu　　set ts-4
3. 可以配置一个python3

### 命令模式 / 底行命令模式 / 编辑模式

### 命令模式
1. G / gg 文末 文首 
2. ct + f / b 翻页　　
3. 4yyp 复制
4. u　撤销
5. 4dd / dw　删除行 删除单词
6. 宏 qa      q   100@a  
* 命令模式下，qa 开始录制
* 简单操作
* q 结束录制
* 100@a  将录制的动作执行100次。

### 底行命令模式
* w! / q! 强行输入和强行退出
* %s/x/y/g  将全文中的x 替换为y,  g全局 i忽略大小写　　% = (1, $)  
* set nu / nonu 设置是否有行号

### 编辑模式
* 注意空格 conding:utf-8 万国码编译

## nginx
*  Nginx -- HTTP server 当服务器使用-静态页面。 wsgi 网关--动态页面

### 安装
1. yum install nginx
2. 将 /usr/share/local/html/index.html 换成自己的网页，就可以通过公网IP访问。
* 阿里云和自己的防火墙上都要开放相应的端口。
* 链接前需要开启nginx

##  mysql
* RDB / Persistence / SQL -- 数据持久化 能存储，能取出。保证数据正确有效，Cluster 多个服务器当跑一个任务，集群 + Load Balance(Nginx / LVS)  负载均衡  + Keepalive  热备，双活。
# 安装

### 安装
1. yum install mariadb mariadb-server 安装客户端和服务器
2. systemctl start mariadb 启动客户端

### 特点
1. 不区分大小写
2. not null 非空约束，不能为空
3. varchar(20)  变长字符串，varible charactor, 最少一个字符，最多20个字符。
4. 命名规则，见名知义，前缀
5. 句内注释 comment '注释'  句外注释 -- 注释
6. 不能用双引号，只能用单引号。
7. 数据以表格的形式出现；
8. 每行为记录名称；
9. 每列记录名称所对应的数据域
10. 列和行组成一张表单
11. 若干的表单组成database;

### 连接
1. mysql -u root -p 连接自己
2. mysql -h id -u 用户名 -p 连接别人

### 使用
1. show databases; 查看有哪些数据库
2. create databases
3. 字符串类型
* char varchar tinyblob tinytext blob text很长的描述型的东西，备注
4. create 创建表
* not null 不为空   unique 
* into_increment 自增 一般用于主键。
5. drop 删除表
* drop table if exists ...
6. alter 更新表
* alter table ... add ...
7. insert into ... set ... 插入数据
8. delete from ... where ... 删除数据
9. updata ... set .. where .. 更新数据
10. select ... from ... where .. 查询

##redis  REmote Dlctionary Server

### 简介
1. 是一个有Salvatore Sanfilippo写的key-value存储系统
2. 它时一个开源的使用ANSI C语言编写 遵守BSD协议 支持网络 可基于内存持久化的日志型 key-value数据库，并提供多张语言的API
3. 通常被称为数据结构服务器，因为值values可以是 String Map list sets sorted sets等类型

### 特点 
1. 支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用
2. 支持key-value list set zset hash等数据结构的存储
3. 支持数据的备份，即master-slave模式的数据备份

### 优势
1. 读 110000次/秒  写81000次/秒
2. 支持二进制的Strings, Lists , Hashes, Sets, Ordered Sets
3. 原子 -- 原子性。
4. 支持 publish / subscribe , 通知 ， key 过期等特性

### 使用redis redis-client

1. 启动
* redis-server   /  redis-cli进入。
2. 后台运行
* redis-server &
3. vim /etc/redis.conf  进入redis的配置文件 
* ：/requirepass  正则查找密码，设置
4. redis-server --help
    redis-server
5. 访问指定IP: 端口的redis服务器
* redis-cli -h ip -p 端口
* 例子  redis-cli -h 172.26.77.93 -p 6379
7. redis 五大类型； string类型  hash list set dict
* set p 1 设置 p 的值为1
* get p   获取p 的值
* incr p  整数递增 ，默认值是零
* decr p  整数递减，用在抢票的时候。

### string 字符串
* 最基本的数据类型，可以包含任何数据，一个键最大存储512MB
* 使用 set 和 get 命令。

### hash  哈希
* 键值对集合 key => value
* 特别适合存储对象，每个hash可以存储2^32-1
* 使用 hmset 和 hget 命令

### list  列表
* redis列表是简单的字符串列表，按照插入顺序排列，你可以添加一个原色到列表的头部或尾部
* 可以存储2^32-1

### set 集合
* set 是 string 类型的无序集合
* 集合是通过哈希表实现的，所以添加， 删除，查找的复杂度都是0
	
