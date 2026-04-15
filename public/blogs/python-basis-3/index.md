# 异常处理有什么用?

可以不让控制台报错, 并且让用户更清晰了解自己错在哪.

```python
try:
    2 / 0   # 因为除数为0, 会报错ZeroDivisionError
except ZeroDivisionError:
    print("除数不能为0")
# except... 这里可以接收更多的异常
else:
    print("没有异常")   # 如果程序没有异常才会执行else语句
finnaly:
    print("有无异常都打印")   # 不管程序是否有异常都会执行finnaly
```

还有更有用的raise关键字, 程序原本没错, 但我可以抛出一些字有意义的自定义错误.

```python
gender = input("输入你的性别: ")

try:
    if gender != '男' or gender!= '女':
        raise Exception("输入的性别有误")   # 抛出异常
    else:
        print(f"你的性别是{gender}")
except Exception as e:
    print(e)
```

# 函数有什么用?

## 怎么使用函数?

函数可以将一段实现功能的代码包装起来, 可以重复使用, 这样使用起来很方便.

如何定义一个函数?

```python
def 函数名称(参数列表):
	函数体
	[return 返回值列表]   # return可以没有
```

如何调用呢?

```python
函数名称(参数列表)
```

如何传参? 四种方式: 位置传参, 关键字传参, 默认值传参, 可变传参.

```python
def fun(name, age):
	print(name, age)
	
# 位置传参, 其实就是参数位置一一对应
fun('L', 18)

# 关键字传参
fun(age = 18, name = 'L')

# 默认值传参
def fun2(name, age = 18)   # age有个默认值
fun2('L')

# 可变传参
fun(*para)   # *para是指任意个数参数
fun2(**para)   # **para是指任意个数键值对
```

## 局部变量 vs 全局变量

什么是局部变量?  --> 定义在参数列表处和函数内部的变量.

什么是全局变量? --> 定义在函数外的变量或者定义在函数内用**global**关键字修饰.

```python
# 局部变量
def fun(a, b):   
	s = a + b   # a, b, s都是局部变量
    
# 全局变量
m = ''
def fun2(x, y):
    global n   # x, y是局部变量. m, n是全局变量
```

## 如何实现匿名函数?

什么是匿名函数? 就是没有名字的函数, 又称lambda函数

如何书写呢? 只能写成一行.

```python
res = lambda a, b: a + b
print(res(1 + 2))
```

## 如何实现函数递归?

什么是函数的递归? 就是函数调用自己, 但是必须要有终止条件, 不然会一只调用会报错.

著名的斐波那契数列如何同归函数递归实现?

```python
def fun(num):
    if num == 1 or num == 2:
        return 1
    else:
        return fun(num - 1) + fun(num - 2)
```

## 常用的内置函数

数据类型转换函数: 

- bool(obj): 获取对象obj的布尔值.

- str(obj): 将obj对象转成字符串类型.

- int(x): 将x转成int类型.

- float(x): 将x转成float类型.

- list(sequence): 将序列转成列表类型.

- tuple(sequence): 将序列转成元组类型.

- set(sequence): 将序列转成集合类型.

常用的数学函数:

- abs(x): 获取x的绝对值.

- divmod(x, y): 获取x与y的商和余数.

- max(sequence): 获取sequence的最大值.

- min(sequence): 获取sequnce的最小值.

- sum(iter): 对可迭代对象进行求和运算.

- pow(x, y): 获取x的y次幂.

- round(x, d): 对x进行保留d位小数, 结果四舍五入.

常用的迭代器操作函数:

- sorted(iter): 对可迭代对象进行排序.

- reversed(sequence): 反转序列生成新的迭代器对象.

- zip(iter1, iter2): 将iter1和iter2打包成元组并返回一个可迭代的zip对象.

- enumerate(iter): 根据iter对象创建一个ennumerate对象.

- all(iter): 判断可迭代对象iter中所有元素的布尔值是否都为True.

- any(iter): 判断可迭代对象中所有元素的布尔值是否都为False, 全为False结果才为False.

- next(iter): 获取迭代器下一个元素.

- filter(function, iter): 通过指定条件过滤序列并返回一个迭代器对象.

- map(function, iter): 通过函数function对可迭代对象iter的操作返回一个迭代器对象

其他函数:

- format(value, format_spec): 将value以format_spec格式进行显示.

- len(s): 获取s的长度或s的元素个数.

- id(obj): 获取对象的内存地址.

- type(x): 获取x的数据类型.

- eval(s): 去掉字符串s左右的符号.

# 什么是面向对象?

## 面向过程 vs 面向对象

面向过程 --> 功能上的封装处理.

面向对象 --> 属性和行为上的封装处理

## 类 vs 对象

对象其实就是类的实例.

如何创建类和对象?

```python
class Student:   # 创建一个类
    def __init__(self, name, age):   # __init()__方法创建实例属性
        self.name = name
        self.age = age
        
    def show(self):   # 实例方法
        print(f'我是{name}, 今年{age}')
        
    @staticmethod   # 装饰器修饰, 这是一个静态方法    
    def info():
        print('这是类Student')
        
    @classmethod   # 装饰器修饰, 这是一个类方法
    def fun_cls(cls):
        pass
    
stu = Student('L', 18)   # 创建一个实例(对象)
stu.show()   # 通过对象调用方法

stu.gender = '男'   # 动态绑定实例属性
def fun():
    print('动态绑定实例方法')
stu.cls_fun = fun   # 动态绑定实例方法
```

## 面向对象三大特征

### 封装

什么是封装?

将内部信息藏起来, 向外提供操作.

如何实现?

```python
class Student:
    @property   # 这个方法来获取gender
    def gender(self):
        return self.__gender
    
    @property.setter   # 这个方法来修改gender
    def gender(self, value)
    	if value != '男' and value != '女':
            print("性别有误, 已将性别设置成默认值男")
            self.__gender = '男'
        else:
            self.__gender = value
```

### 继承

什么是继承?

继承就是儿子可以用父亲的东西, 如果不喜欢可以重写.

如何实现?

```python
class Father:
    def show(self):
        print('我是一个类')
        
    def info(self):
        print('我是你爹')

class Son(A):
    def show_son(self):
        super().show()
        
    def info(self):
        print('我是你儿子')
        
class Grandson(Son, Father):   # 一个子类可以继承多个父类
    pass
```

### 多态

什么是多态?

多态就是一个方法, 不同的对象实例, 利用这个方法实现不同的功能.

如何实现?

```python
def Person:
    def eat(self):
        print('我要吃饭')
        
def Dog:
    def eat(self):
        print('我要吃shi')
        
def Cat:
    def eat(self):
        print('我要吃猫粮')
        
p = Person()
d = Dog()
c = Cat()

p.eat()
d.eat()
c.ear()   # 它们通过同名的方法实现了不同的功能
```

### 变量赋值 vs 浅拷贝 vs 深拷贝

三者内存变化有什么区别?

变量赋值 --> 只是形成两个变量, 实际上还是指向**同一个对象**.

浅拷贝 --> 拷贝时**对象包含的子对象不拷贝**, 因此源对象与拷贝对象会引用一个子对象.

深拷贝 --> 使用copy模块的deepcopy函数, 递归拷贝对象中包含的子对象, **源对象和拷贝对象所有的子对象也不相同**.

![](/blogs/python-basis-3/8d9a61f6a3c65d8b.png)

# 模块及第三方模块

什么是模块? 

就是你平常常见的以.py为后缀的文件.

模块如何导入?

两种方式: import 模块名 as 别名, from 模块名 import 变量, 类, *

导入模块有什么用?

可以导入一些别人早就写好的模块, 然后使用提高开发效率.

如何导包?

两种方式: import 包名.模块名 as 别名; from 包名 import 模块名 as 别名

什么是主程序运行?

if \_\_name\_\_ == '\_\_main\_\_': pass, 主程序运行, 可以阻止导包时数据被输出执行.

如何安装与卸载第三方模块?

打开win + R 打开cmd, 输入pip install 模块名称进行安装, 输入pip install 模块名进行卸载.

# 总结

今日学习内容: 异常处理(try...except...else...finally, raise), 函数及常用的内置函数(如何使用函数? 作用域, 匿名函数lambda, 递归, 常用内置函数), 面向对象(什么是类和对象? 面向对象三大特征, 深浅拷贝), 模块与第三方模块(如何导入模块和包? 如何安装第三方模块?)