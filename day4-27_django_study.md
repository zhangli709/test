
# cookie
1. set_cookie()
2. del_cookie()

## 注册 登录 注销

1. 注册
* 常规操作，将其存储在数据库中。
2. 登录
* 常规操作，将其与数据库之中的数据对比，如果正确，那么将其保存在cookie中。
* 做法
* res = HttpResponse()
* res.set_cookie('xx', xx)  此处xx为键值对，
将cookie保存在数据库里，save一下。
3. 验证跳转  COOKIES
* 就是想要访问此网站，必须先验证此cookie是否和数据库里的cookie相等，相等才允许访问。
* ticket = request.COOKIES.get('ticket')



* 向数据库里保存值，两种方法。用create方法，直接在创建时就保存了，用常规赋值方法的话，需要用save()方法。

# 跳转的几种方法 -->views
1. HttpResponseRedirect('/uauth/login/')
2. HttpResponseRedirect(
            reverse('s:addinfo', kwargs={'stu_id': stu.id})
        )
3. HttpResponse('用户名或密码错误')
4. render(request, 'register.html')

# 跳转之html--> a
1. <a href="/s/allstu/{{ g_id }}/">
2. <a href="{% url 's:alls' g.id %}">

# urls 里带参跳转
1. url(r'^addStuInfo/(?P<stu_id>\d+)/', views.addStuInfo, name='addinfo'),