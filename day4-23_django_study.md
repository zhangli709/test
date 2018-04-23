
# Django
* Python下的一个Web框架，最好用的一个，是开放源代码的Web应用框架。
* 遵守BSD版权，采用MVC的软件设计模式，M模型 V视图 C控制器
* C 处理用户的请求
* M 模型对象在数据库增删改查
* V 返回图形界面
* 流程   U --> C --> M --> C --> V 

## Django模式简介
* M V T
* Model 负责业务与数据库（orm)的对象
* View 负责业务逻辑并适当调用Model 和Template
* Template 负责吧页面渲染展示给用户
* 注意：Django中还有一个url分发器，也叫路由，主要用于将不用的URL交给不同的view的处理
* 流程   U --> (urls) -->  C --> M --> C --> T

## 扩展概念
1. MVC
2. MVT
3. B/S 浏览器 / 服务器
4. C/S client / server

## 如何手动安装python的坏境
1. pip3 install virtualenv  安装虚拟坏境
2. virtualenv --no-site-packages -p python3的路径 env  安装坏境到指定目录，安装env坏境。
3. 进入到坏境的Scripts/activate中，执行 pip install pymysql 安装数据库
4. 退出 deactivate

## 安装Django 
* pip install django==1.11   加等号相当于安装哪个版本


### Linux 上安装Django
1.yum安装方法 （Centos Linux)
* yum install python-setuptools
* easy_install django
2. pip 安装方法
* pip install Django

## Djagno创建第一个项目
### Django 管理工具 django-admin.py
### 创建第一个项目
1. django-admin startproject hello_world  创建
* 创建之后可以进入pycharm中，进行开发，但须配置坏境
* file -- settings -- Project interpreter --用自己配置的坏境。
2. cd hello_world/ 
3. tree 查看
4. python manage.py runserver id:端口 启动服务器，让任何人可以连接
* 可在浏览器输入IP和端口号登入
5. settings
* DEBUG   开发时为True, 上线时为False
* LANGUAGE_CODE = 'zh-hans'  修改为中文
* TIME_ZONE = 'UTC' 相比北京时间少8个小时。 改为 'Asia/Shanghai'
6. python manage.py startapp appname 创建app
7. app的结构
*  __init__.py:初始化
*  admin.py:管理后台注册模型
*  apps.py:settings.py里面注册app的时候推荐使用
*  from app.apps import AppConfig
*  AppConfig.name
*  models.py: 写模型的地方
*  views.py: 写处理业务逻辑的地方
8. 展示网页方法
    1. 没有创建app时，启动主应用，manage.py,默认开启8000端口，可以通过id:8000访问。
    2. 创建app时，例如创建一个app.
    * app里：
    * 创建并在urls里写入搜索连接
    * 在views里写入 urls关联的在页面显示的内容
    * 主文件里；
    * settings里，在INSTALLED_APPS里添加app名字，
    * urls中，填入app搜索的地址连接，变为去app里搜索。
    * 最后即可通过id:端口/app/关键字
9. 迁移数据库
    1. 首先创建一个app,名字称为stu.
    2. stu里：
    4. 创建并在urls里写入搜索连接
    5. 在views里写入 urls关联的在页面显示的内容，写入数据库的内容。
    6. 在models里写入将写入数据库的内容的类型。
    7. 主文件里：
    8. 在init里，导入数据库
    9. settings里，在INSTALLED_APPS里添加app名字，在DATABASES里写入连接数据库的操作。
    10. urls中，填入app搜索的地址连接，变为去app里搜索。
    11. 在数据库只需建立一个空数据库，让其连接，即可通过连接修改内容了。
    12. python manage.py makemigrations
    13. python manage.py migrate
    11. 最后即可通过id:端口/app/关键字


























### 视图和url配置
1. 在HelloWorld目录新建一个view.py文件，
* from django.http import HttpResponse
* def hello(request):
    return HttpResponse("Hello world!")
2. 绑定URL与视图函数，打开urls.py,修改代码如下
* from django.conf.urls import url
* from . import view
* urlpatterns = [
	url(r'^$', view.hello),
  ]
3. 访问开发服务器，视图已经改变
4. url()函数， 可接受四个参数,前两个为必选，其他为可选
* regex: 正则表达式，与之匹配的URL会执行对应的第二个参数view
* view; 用于执行与正则表达式匹配的URL请求
* kwarge;视图使用的字典类型的参数
* name: 用来反响获取URL

## 模板
* 模板是一个文本，用于分离文档的表现形式和内容

### 模板应用实例
1. 在HelloWorld目录下创建templates目录，并建立hello.html文件，
* <h1>{{hello}}</h1>
2. 修改设置里的路径，setting.py
* 修改TEMPLATES中的DIRS为 [BASE_DIR+"/templates",]
3. 修改view.py,增加一个新的对象，用于向模板提交数据
* # _*- coding:utf-8 _*_
* # from django.http import HttpResponse
* from django.shortcuts import render
* def django.http import render
* def hello(request):
      context = {}
      context['hello'] = 'Hello World!'
      return render(request, 'hello.html', context)

## 模板标签
### if / else 标签
1.  {% if condition %}
		... display
	{% endif %}
2. {% if condition1 %}
		... display 1
	{% elif condition2 %}
		... display 2
	{% else %}
		...display 3
	{% endif %}
3. for 标签
* for x in y
4. ifequal / ifnotequal 标签
5. 注释标签 {#注释#}
6. 过滤器 {{ name | lower}}
7. include 标签 {% include "nav.html" %}
8. 模板继承

## Django 模型
* 支持多种数据库

### 数据库配置
* settings.py 中的 DATABASES修改信息

### 定义模型
#### 创建APP
* 规定，要使用模型，必须创建一个app.
1. django-admin.py startapp TestModel
2. 修改TestModel/models.py
* from django.db import models
* class Test(mdels.Model):
      name = models.CharField(max_length=20)
3. 接着在settings.py中找到INSTALLED_APPS这一项，
* INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'TestModel',               # 添加此项
  )
4. 在命令中执行；
* python manage.py migrate 创建表结构
* python manage.py makemigrations TestModel 让Django知道我们做了变动
* python manage.py migrate TestModel 创建表结构

### 数据库操作
* 添加testdb.py,并修改urls.py'

#### 添加数据
1. 创建对象，执行save函数，

#### 获取数据
#### 更新数据
* save()  update()
#### 删除数据
* delete()

## 表单
* 交互行为

### HTTP请求

### GET 方法

### POST 方法

### Request 对象

### QueryDict 对象

## Django Admin 管理工具

### 激活管理工具
### 使用管理工具
### 复杂模型
### 自定义表单
### 内联（inline) 显示
### 列表页的显示

## Django Nginx+uwsgi 安装配置

### 安装基础开发包
1. Centos 
* yum groupinstall "Development tools"
* yum install zlib-devel bzip2-devel pcre-devel openssl-devel
* ncurses-devel sqlite-devel readline-devel tk-devel 

