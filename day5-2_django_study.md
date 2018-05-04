# 登录 注销 深度学习

1. set_cookie(key, value,max_age=10)
* max_age 存活时间
2. 加载static
* {% load static %} {% static %}
*  /static/xxx.css
3. delete_cookie(key)

## 配置静态文件
1. settings
* STATIC_URL = '/static/'
* STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
2. 一般都是放html里的样式，例如css/img/js这几个，修饰templates/html

## 上传图片
1. settings的配置
* MEDIA_URL = '/media/'
* MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
2. pip install pillow 安装包。
3. html中form中加enctype="multipart/form-data"
4. 在主urls中，
* from day27_1 import settings
* urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
5. 在app里的models.py 中，即数据库里保存图片，
* i_image = models.ImageField(upload_to='upload',null=True),之后更新数据库
6. 在网页addStu里增加图片的存入操作，
* <input type="file" name="img">
7. 在views里通过request方法拿到图片，并保存到数据库里。（保存的是路径）
8. 通过views方法，在数据库里去读取路径，
9. 在网页里通过画一个img, 并通过路径读取，在页面里显示图片
* <img src="/media/{{ stuinfo.i_image}}" alt="">

## 面向切面编程 AOP
1. process_request: 在处理URL路由之前进行处理逻辑
2. process_response: 在响应返回浏览器之前调用
3. process_view: 调用视图之前调用
4. process_templates_resposne：在视图刚好执行完的时候调用

### 应用-->中间键
1. 创建一个文件夹utils，文件夹里创建一个py文件，在文件里写入在执行任何文件前都要执行的操作。这里是进行cookie的验证。
2. 在settings里的中间键里添加链接。即中间键的路径。
3. 文件里写入的具体操作
* class AuthMiddleware(MiddlewareMixin):
*     def process_request(self, request):

## 埋点
seo url 点击率
作业 统计添加学生的点击次数 url/stu/addStu pos 请求的次数

## 分页 Paginator(key, num)   如下例子。
Paginator对象：
	page(number): 展示第几页
	count(): 总共多少条数据
	num_pages:总共多少页  总 / num
	page_range：遍历时使用
	* for i in stus.paginator.page_range
page对象
	has_next:是否有下一页
		next_page_number:下一页
	has_previous:是否有上一页
		previous_page_number:上一页
	number 当前是多少页
<!-- page_id = request.GET.get('page_id')
        stus = Student.objects.all()
        paginator = Paginator(stus,1)
        page = paginator.page(int(page_id))
        return render(request, 'fen_ye.html', {'stus': page})

<h4>一共{{ stus.paginator.num_pages }}页/ 一共{{ stus.paginator.count }}条</h4>
<h5>{% for i in stus.paginator.page_range %}
    <a href="/stu/stuPage/?page_id={{ i }}">{{ i }}</a>
{% endfor %}</h5>
{% if stus.has_previous %}
    <a href="/stu/stuPage/?page_id={{ stus.previous_page_number }}">上一页</a>
{% endif %}
当前第{{ stus.number }}页
{% if stus.has_next %}
    <a href="/stu/stuPage/?page_id={{ stus.next_page_number }}">下一页</a>
{% endif %}
 -->

