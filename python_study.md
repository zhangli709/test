# Python3
## Python简介
1. Python是一种解释性语言，最大的优点：可以跨平台使用，开发效率高。 最大的缺点：执行效率低。

2. 今天计算机已经足够发达，我们追求的更多的是程序的开发效率，而不是执行效率。

3. Python的官网：http://python.org

4. 我们可以使用Python的包管理工具pip来安装第三方插件。

* 说明：如果要在Linux环境下更新到Python3.x版本，需要通过源代码来实现。

* ```Shell
* pip install ipython jupyter
* ```

* ```Shell
* Python -m pip install ipython jupyter
* ```

5. 第一个Python程序 hello world!

* """
* 第一个Python程序
* Version:0.5
* Author:张立
* Date:2018-3-2
* Modifier:王大锤
* Date:2018-4-5
* """
* print('hello, world!)
6. 如果想在交互式环境中进行Python开发，用ipython 和jupyter均可

## 变量
1. 变量的作用：变量是数据的载体
2. 变量的命名规则：
    1. 由数字,字母和下划线组成,且不能由数字开头。
    2. 不能用关键字命名,不能用特殊字符。
    3. 区分大小写，大写为常量。
3. 变量的类型：

## 运算符
1. 赋值运算符 =
2. 算数运算符
* +  -  *  /  //  %  **（求幂）
3. 关系运算符
*    <   <=   >   >=   ==   !=
4. 逻辑运算符
*   and   or   not（逻辑变反）
5. 身份运算符 is

## 分支结构*
1. 分支语句末尾以冒号结尾
2. 下一行缩进4分空格。
* 九九乘法表举例。

## 循环结构
1. for循环，用于已知次数的循环
2. while 循环，用于未知次数的循环。

## 函数
* 我们可以把程序中相对独立的功能模块抽取出来，这样的好处是可以减少重复代码的编写，将来可以重复使用这些功能模块，Python中的函数就是代表了这样的功能模块。
* 命名：age_of_student(官方） 或 ageOfStudent(大部分人的习惯用法，又称驼峰命名法）
* 调用： import 模块 （as 别名）  函数名（参数）
* 注意：二元运算符之间放空格，参数里赋值时，等号两边不加空格。例如：def f(x=2)　

## 可变参数的函数
* def add(*args): #*args可变参数，个数不确定。
      total = 0
      for value in args:
          total += value
      return total

## 递归函数
1. 收敛条件 - 让递归在有限的次数内完成或者进行回溯
* 如果递归无法在有限的次数内收敛，就有可能导致RecursionError
2. 递归公式
* 十级楼梯，走完十级台阶有几种走法。每次走1到3步。
* def walk(n):
*     if n < 0:
*         return 0
*     elif n == 0:
*         return 1
*     return walk(n-1) + walk(n-2) + walk(n-3)
* if __name__ == '__main__':
*     print(walk(25))

## 生成器函数
* def fib(n):
*     a, b = 0, 1
*     for _ in range(n):
*         a, b = b, a + b
*         yield a
* f = fib(20)
* print(f)
* for val in fib(20):
*     print(val)

##  函数的作用域
1. 在函数外面，叫做全局变量 global variable
2. 减少全局变量的使用，尽量使用局部变量。迪米特法则：不要和陌生人说话，尽量让模块之间不要发生联系。
3. Python搜索一个变量的方式是从局部作用域到嵌套作用域再到全局作用域，最后到内置作用域。即 local > enclose>global>built-in(l e g b)
4. 如果想改变搜索范围，可以使用global 和nonlocal关键字。
* a = 100
* def foo():
* 函数内的局部变量，离开foo函数时无法访问的。 local variable
*     global a
* 提升权限，变为全局变量，可以直接修改，重新定义申明的变量。
*     a = 200
*     print(a)
*     b = 'good'
*     def bar():
*         nonlocal b
*         #  非局部作用域。
*         b = 'hello'
*         print(b)
*         print(a)
*     bar()
*     print(b)
* foo()
* print(a)

## 函数的存储类型
1. 分为3大类，栈--stack，堆--heap,(数据段，只读数据段，代码段）-静态区
2. 函数调用时，变量是放在内存小，执行快的栈上面的，对象是放在内存无穷大的堆上面的。
3. 变量--对象的引用--放的是对像的地址。  对象--放在堆上面。
4. 函数调用时，会经过保存现场和恢复现场两个操作。在进入函数调用前，要保存当前的执行现场，函数的执行现场是保存在栈上，执行--先进后出的存储结构。
 
##  tips
* ctrl + q    当前位置查看注释，
* ctrl + lb    返回写注释位置查看注释
* shift + F6  重命名
* 字符串倒过来的做法：[-1::-1]

## 字符串 string 
### 转义字符
* \行尾时，续航符 
* \n 换行   \t横向制表符   \v 纵向制表符

### 字符串运算符
1.   + 字符串连接
2.   * 重复输出字符串
3.   [] 切片
4.   in 判断是否属于，返回布尔值
5.   r/R  转义
6.   % 格式字符串，很重要，占位什么的。

### 字符串格式化
1. %2d  整数
2. %.2f 小数
3. %10s  字符串
4. 辅助指令
*   - 左对齐
*   + 正数前显示加号
*   <sp> 正数前显示空格
*   0  显示的数字前面填充0而不是默认的空格

### Python三引号
* 允许字符串跨多行

### 字符串的内建函数
1. 增  +  
2. 删 remove(str)  pop()  
3. 查 find(str) index(str)  endwith(str) startwith(str) 
4. 改  [-1::-1]  [2::2]  [2:4]
5. 其他用法
* isdigit 判断是否全是数字
* isalpha 判断是否全是字母
* isalnum 判断是否全是数字和字母
* strim   lstrim   rstrim  去掉空格
* count(str) 次数  len(str) 长度
* split(str) 分割

## 列表 
* 最基本的数据结构，序列中的每一个元素都分配一个数字，它的位置，或索引，第一个索引是0，以此类推。可以进行索引，切片，增，减，查。它是由方括号和逗号分隔来实现的。
* 创建： list(), [1, 2, 3, 4], [x for x in range(6)]

### 访问列表中的值
* 访问下标

### 更新列表
* list[2] = new_word

### 删除列表元素
* del list

### 列表函数方法
1. 增 list.append(obj) list.insert(index,obj)  
2. 删 list.reverse()  list.pop() 
3. 改 list[index] = obj
4. 查 list.find()  list.index()
5. 其他命令
* count()  len()  list.sort()对原列表排序  newlist = sorted(list)  list.reverse() 反向排列

## 元组
* 同列表，但是元组的元素不能修改，元组使用小括号， 列表使用方括号

### 创建
* tup1 = ('hello',)
* tup2 = ()

### 访问
* tup1[index]

### 修改
* 不能修改，但是能连接组合
* tup3 = tup1 + tup2

### 删除
* 不能删除单个元素，但是能删除整个元组
* del tup

### 元组运算符
*  len()  +   *    in    for x in tup: 迭代

### 切片 
* 获取片段，得到新元组

### 元组的内置函数
* min  max  tuple()  len()

## 字典
* 可变容器，可以存储任意类型
* 每个键值（key=value)用冒号分割，每个对之间用逗号分割，整体用花括号。
* 键必须时唯一的

### 访问
* dict['key']

### 修改
* dict['key'] = new_word  有则更新，无则添加

### 删除
* del dict 
* del dict['key']

### 内置函数和方法
1. len() 键值对的总数
2. str(dict) 输出字符串式的字典
3. type()
4. 增 dict.update(dict2) 
5. 删 dict.clear()  pop(key)   popitem() 
6. 改
7. 查 dict.get(key)  key in dict 
8. dict.items 遍历    for key,val in dict.items
9. dict.values 以列表形式返回字典中的值。

## 集合
* 由大括号和逗号，组成，元素不可重复，且无序排列，无下标。

### 内置函数
1. set.add()
2. set1.intersection(set2) 差集
3. set1.union(set2) 并集
4. set1.difference(set2) 差集
5. set1.symmetric_difference(set2)  对称差
6. remove()
7. pop()

## 面向对象
* 类名，每个单次首字母大写，且要有属性和行为

### 类的定义
1. 类是对象的蓝图和模板，有了类就可以创建对象
2. 定义类需要做两件事情：数据抽象和行为抽象
3. 数据抽象：抽取对象共同的静态特征（找名词）- 属性
4. 行为抽象：抽取对象共同的动态特征（找动词）- 方法
* 定义类的关键字- color-类名（每个单词首字母大写）

class Student(object):
	def __init__(self,name,age):
		self._name = name
		self._age = age
	def study



