
# 笔记

## 任务，实现闪购

## datetime, timedelta
from datetime import datetime, timedelta
1. timedelta(days=1)
2. timedelta(hours=1)
3. timedelta(minutes=1)

中间键，过期时间，
response.set_cookie('ticket',ticket,max_age=3000)

out_time = datetime.now() + timedelta(days=1)
response.set_cookie('ticket',ticket,expires=out_time)

## 传参
reverse('', args=('','',''))
* 一般排序有几种方法赛选，就代表要传入几个参数，来进行排序赛选条件。

* 一般来说，最开始跳转时，给点跳转链接，给予这几个参数一个默认值，传入新的链接里，
* return HttpResponseRedirect(reverse('axf:show', args=('1','2','3')))

1. 在app的urls里，模糊传参，要传入几个参数，就
* url(r'^show/(\d+)/(\d+)/(\d+)', views.show)  表示传入3个参数。
2. 在对应的views方法里，要接收这3个参数
* def show(request, typeid, cid, sort_id):
	<!-- 使用之后，记得返回参数， -->
	data = {
	'typeid': typeid,
	'cid': cid,
	'sort_id': sort_id
	}

	return render(request, 'html', date)
3. 在网页里接收这些参数，因为是三级查询排序，
对于第一个接收的查询，
* 给予第一个点击变化的参数，后两个给于默认值。
* 对于第二个查询，变化第二个参数，第一个参数定为第一个参数最后一次变化的参数，即传入形参，第三个参数给予默认值
* 查询第三个时，第一个和第二个最后一次的值，作为参数传入，即传入形参，第三个参数传入对应变化的值。


## ajax 实现购物车的增删，调用数据库里的值，进行查询，然后返回到页面
1. 通过点击，返回一个js方法，带参传入js方法中
* onclick="btn1({{id}})"
2. 在js中接收参数，把参数传入到url链接的那个函数中
* function btn1(id){
	csrf = $('input[name="csrfmiddlewaretoken"]').val()
	$.ajax({
		url: '/goods/show/',
		type: 'POST',
		data: {'id':id},
		dataType: 'json',
		headers:{'X-CSRFToken':csrf}
		success: function(msg){
		<!-- 这里一般拿到页面的某个区域的id，然后在这个区域里渲染我们想要渲染的东西。 -->
			$('#') 
		},
		error: function(){
			alert('请求失败')
		}
	})
}
3. 在views方法中，接收ajax传入的参数，并进行方法的实现。
* def show(request):
      if request.method == 'POST':
          data = {
          'code': 200,
          'msg': '请求成功'
      	  }
      	  user = request.user
      	  id = request.POST.get('id')
      	  if user and user.id:
      	  	  data['is_select'] = 1
      	      pass
      	  return JsonResponse(data)
4. views 方法查询数据库，把查询到的数据返回json格式的数据到ajax中
5. 在ajax方法的success方法中，用来实现渲染效果。
* success: function(msg){
	if (msg.is_select){
		s = '<span onclick="changeselect(' +  id + ')">√</span>'
	}else{
		s= '<span onclick="changeselect(' + id + ')">x</span>'
	}
	$('#id' + 参数).html(s)
 }

