
## django 自带的登录方法
1. 第一步同理先拿到用户名和密码
2. 引入django自带的包auth,   from django.contrib import auth
* user = auth.authenticate(username=name, password=password) 如果数据库里存在数据，则返回user,否则返回的为空。
3. if user:
*  auth.login(request, user) 自带的方法直接登录，在登录的时候，同时在数据的里保存了ticket一样的东西，他保存在session里，过期时间为两周。
4. 让所有的网页在没有登录时都失效，需要在url前加上
* url(r'^index/',login_required(views.index)),

## django自带的注册方法
1. from django.contrib.auth.models import User 引入django自带的用户表，
2. User.objects.create_user(username=name,password=password) 将网页传入的用户名和密码保存在数据库里。

## django自带的注销方法
1. auth.logout(request)

## 复习总结
1. cookie/session
2. 加密/解密
3. 中间键
4. reverse 页面跳转
5. url if for 
6. 登录注册（自带的，与原生的）
7. 上传文件

## 统计url访问的次数
* 方法,中间键
1. path方法，即所有的路径
2. 做法：有此路径，则访问次数加一，如果没有此路径，就创建此路径，并给予次数1
 <!-- path = request.path
        try:
            visit = Visit.objects.get(v_url=path)
            if visit:
                visit.v_times +=1
                visit.save()
        except Exception as e:
            print(e)
            Visit.objects.create(v_url=path,v_times=1) -->

## postman的学习使用
1. www.getpostman.com下载。

### postman在项目中的框架写入
1. 在app的urls中写入跳转链接
* from rest_framework.routers import SimpleRouter
* router = SimpleRouter()
* router.register(r'student', views.StudentEdit)
* urlpatterns += router.urls
2. 在app中新建一个serializers.py的文件，并写入如下代码
* from rest_framework import serializers
* from stu.models import Student 调用数据库里的student这个数据库
* class StudentSerializer(serializers.ModelSerializer):
*	class Meta:
*		model = Student
*		fields = ['id','s_name','s_tel'] 在页面显示的内容
* 	def to_representation(self, instance):
*		data = super().to_representation(instance)
*		try:
*			data['s_addr'] = instance.studentinfo.i_addr
*		except Exception as e:
*			data['s_addr'] = ''
*		return data
3. 在app的views方法里，写入,注意，这里是一个类！！
* from stu.serializers import StudentSerializer
* class StudentEdit(mixins.ListModelMixin,
* 					mixins.RetrieveModelMixin,
*	                mixins.UpdateModelMixin,
*	                mixins.CreateModelMixin,
*	                mixins.DestroyModelMixin,
*	                viewsets.GenericViewSet):
*	queryset = Student.objects.all() 查询所有信息
*	serializer_class = StudentSerializer  序列化
4. 即可通过在postman软件上，通过get post put patch delete进行对数据的可视化操作，增删查改。

## 前后端
1. 前端：vue
2. 后端： restframeork

## 日志的学习 logging

### 四个组成
1. loggers 用来接收传入的信息
2. handlers 用来处理信息
3. filters 过滤loggers传递给handlers的信息，加一些处理控制
4. formatters 格式化，将我们需要保存到日志文件中的信息进行统一的格式化

### 等级划分
1. 错误日志等级划分  CRITICAL > ERROR > WARNING > INFO > DEBUG
* critical 重大的bug
* error 系统里面有错误
* warning 警告
* info 正常
* debug 调试信息

### 日志的创建 （settings)
# 创建日志的路径
LOG_PATH = os.path.join(BASE_DIR, 'log')
# 如果地址不存在，则自动创建log文件夹
if not os.path.isdir(LOG_PATH):
    os.mkdir(LOG_PATH)
LOGGING = {
    # version只能为一
    'version': 1,
    # True表示禁用loggers
    'disable_existing_loggers': False,

    # 1. 保存信息的格式类型定义。
    'formatters': {
        'default': {
            'format': '%(levelname)s %(funcName)s %(asctime)s %(message)s'
        },
        'simple': {
            'format': '%(levelname)s %(module)s %(created)s %(message)s'
        }
    },
    # 2. 处理信息的两种方式
    'handlers': {
        'stu_handlers': {
            'level': 'DEBUG',
            # 日志文件指定为5M,超过5M重新备份，然后写入新的日志文件
            'class': 'logging.handlers.RotatingFileHandler',
            # 最大为5M
            'maxBytes': 5 * 1024 * 1024,
            # 文件地址
            'filename': '%s/log.txt' % LOG_PATH,
            # 按照上面的default格式保存信息
            'formatter': 'default'
        },
        'uauth_handlers': {
            'level': 'DEBUG',
            # 日志文件指定为5M,超过5M重新备份，然后写入新的日志文件
            'class': 'logging.handlers.RotatingFileHandler',
            # 最大为5M
            'maxBytes': 5 * 1024 * 1024,
            # 文件地址
            'filename': '%s/uauth_log.txt' % LOG_PATH,
            # 按照上面的default格式保存信息
            'formatter': 'simple'
        }
    },
    # 3， 用那种方法调用，产生一个接口来调用2
    'loggers': {
        'stu': {
            'handlers': ['stu_handlers'],
            'level': 'INFO'
        },
        'auth': {
            'handlers': ['uauth_handlers'],
            'level': 'INFO'
        }
    },
    # 4. 过滤器，这里不需要
    'filters': {

    }
}


### 日志的使用, 全项目任何地方均可使用
* import logging
* logger = logging.getLogger('stu')
* logger.info('url: %s method:%s获取学生信息成功' % (request.path, request.method))



# 基础知识

## restful风格是什么意思
REST是所有Web应用都应该遵守的架构设计指导原则