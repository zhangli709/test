
# jinjiang

1. {% for stu in stus %} {{ stu.xxx }}{% endfor %}  遍历循环
2. {{ xxx }}  在网页中显示出来的内容，都是双括号
3. {% if xx %}{% endif %}   if 条件判断
4. {{forloop.counter}}  正序，从1开始，添加数字。
5. {{forloop.counter0}} 正序，从0开始，添加数字。
6. {{forloop.recounter}} 反序，
7. {{XXX | add:10}}  数据加10通过页面显示出来
8. {{xxx | add:-10}} 
9. {{xxx | date:'Y-M-D h:m:s'}}  y两位，Y四位， m,d 数字 ,M,D, 英文，  h,m,s,数字。前提是，这个类型为DatetimeField
10. 多行注释   {% comment %} xxx {% endcomment %}   ctl+/  单行注释 
11. {{xxx | upper}} 英文变大写，中文不变 lower--小写
12.  {% widthratio 10 1 xxx %} == {% widthratio xxx 1 10 %}  10 分子， 1， 分母， xx 对象
13. 注意，过滤器不要给空格，不然有的地方会报错。


# 网页跳转
* 从一个链接到另外一个网页，有两个方法。

1. 从真名来找，
* 从 <a href="/s/all/{{xx}}"> 以此来查找对应的views,并且传入参数xx,作为筛选条件，返回数据库里的某些值。
2. 从别名来找，
* 需要在主链接里添加别名，在include里写入，namaspace='x',
* 在对应的app的urls中，name='y',
* <a href="{% url 'x:y' xx %}", 其中xx是参数，一般是两表的链接点的值。
* 其中HttpResponseRedirect  中间跳转的参数。
*  指定参数，/(?P<x>\d+)  x是指定的参数。
3. r'^actstu/(?P<year>\d+)/(?P<month>\d+)/(?P<days>\d+)'  传入多个参数，并指定。
4. 在app里的urls里传不传参，取决于a标签里的写法。
* <a href="/s/upstu/?stu_id={{ stu.id }}"> 不用传参。
* <a href="/s/allstu/{{ g_id }}/">  传参
* <a href="{% url 's:alls' g.id %}"> 传参

# 报错处理
1. handler404 = page_not_found   网址错误就报404
2. handler500 = server_error 	  网址正确，但是内容错误，就报500，都写在主程序的urls中，通过在app的views中写函数，来跳转到404.html或505页面。


# 请求方式
* post 提交数据会隐藏
* get  提交数据在url上，  ?xx=xxxx
* put  更新全部
* patch 更新局部数据
* delete  删除

1. 增加 
* 赋值，提交。
2. 删除 delete()
* get : /s/getstu/s_id/ 
* post: /s/getstu/s_id/
* 删除  Student.objects.filter(s_id = id).delete()

3. 改 update(s=xx)，同删除。


