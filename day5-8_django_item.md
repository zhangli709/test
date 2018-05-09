
# 中间键写ticket以及设置过期时间
from datetime import datetime
def process_request(self,request):
	ticket = request.COOKIES.get('ticket')

	if not ticket:
	#没有令牌，什么也不做
		return None
	users = UserModelInfo.objects.filter(ticket=ticket)

	if users:
	# 判断令牌是否有效
		out_time = users[0].outtime.replace(tzinfo=None)
		now_time = datetime.utcnow()

		if now_time < out_time:
			# 没有失效,用户表可用
			request.user = users[0].t
		else:
			# 删除失效的ticket
			users.delete()

# 表的复习，一对一，一对多，多对多
1. 一对一，子查母，.g    母查子，.子表名
2. 一对多，子查母，.g    母查子，.子表名_set
3. 多对多，子查母，.g    母查子，.子表名_set