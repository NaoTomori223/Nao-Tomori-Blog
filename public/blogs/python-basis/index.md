# 如何控制程序的流程?

- if...elif...else判断语句, 如果其中某一部分满足条件True, 则执行其中的语句块, 并且不会继续往下判断.
- match...: case:...匹配模块(Python3.11), 简单说就是满足哪个case就执行对应的语句块.
- for循环, while循环, 让程序更简单更方便更美观
- break可以直接结束当前循环
- continue停止本次循环, 立刻执行下一次循环
- pass写在没代码的地方, 防止报错

# 实战: 提高动手能力

基于if判断语句, for循环, while循环, match, break, continue完成了以下的实战:

这是一个用户登录界面的模拟, 而且只有三次登录条件.

```python
# 模拟登录界面, 三次登录
user = input("请输入用户名: ")
password = input("请输入密码: ")
count = 1

while count < 3:
    if user == "L" and password == "123":
        print("登陆成功!")
        break
    else:
        print("用户名或者密码错误!")
        user = input("请重新输入用户名:")
        password = input("请重新输入密码: ")
        count += 1
else:
    print("登陆失败, 稍后再试!")
```

这是一个简单的猜数字游戏, 让我熟悉了while循环和if条件的使用. 

```python
"""
猜数字游戏
需求: 随机生成一个1-100的整数, 然后让用户猜, 要提醒猜大了或者小了, 记录用户猜的次数.
"""
target = random.randint(1, 100)
while True:
    entry = eval(input("输入你猜的数字: "))
    if entry == target:
        print(f"恭喜答对了! 答案为{target}")
        break
    elif entry < target:
        print("你猜的数字小了!")
    elif entry > target:
        print("你猜的数字大了")
```

模拟10086服务, 提供了一系列功能操作, 主要亮点: 使用了match模块匹配, 非常方便.

```python
"""
模拟10086查询功能
需求:输入1, 显示当前余额;
输入2, 显示当前的剩余流量, 单位为G;
输入3, 显示当前的剩余通话, 单位为分钟
输入0, 退出自助查询系统
"""

while True:
    choice = eval(input(
        "-------------欢迎使用10086!-------------\n输入1, 显示当前余额\n输入2, 显示当前的剩余流量\n输入3, 显示当前的剩余剩余通话\n输入0, 退出系统\n请输入要执行的操作: "))
    if choice != (0 or 1 or 2 or 3):
        print("请输入正确的数字!")
        continue
    match choice:
        case 0:
            break
        case 1:
            print("当前余额为123元")
        case 2:
            print("当前剩余流量为28G")
        case 3:
            print("当前剩余通话时间为129分钟")
print("下次再见!")

```

# 组合数据类型有哪些?

在此之前, 先回顾一下序列, 序列就是用来存储多个值的连续空间, 并且每个值都对应一个整数编号, 称之为索引. 

索引可以从左到右看0 --> N, 也可以从右往左看, 那就是N <-- -1

一个有用的操作: **切片**. 所谓切片, 就是从原字符串切出一个新的来, 例如:

```python
print("HelloWorld"[0:5:1]) --> Hello
print("HelloWorld"[-10:-5:1]) --> Hello
```

那么有哪些组合数据类型呢? 

列表list[ ], 元组tuple( ), 字典dict{key:value}, 集合set{ }

它们有什么区别?

![](/blogs/python-basis/dc25ed523e0f60bf.png)

list一些常用方法:

```python
lst.append(x)      # 末尾添加
lst.extend(iter)   # 扩展多个元素
lst.insert(i, x)   # 指定位置插入

lst.remove(x)      # 删除指定值（第一个）
lst.pop(i)         # 删除并返回索引元素（默认最后一个）
lst.clear()        # 清空列表

lst.index(x)       # 查找索引
lst.count(x)       # 统计次数

lst.sort()         # 排序（原地）
lst.reverse()      # 反转

lst.copy()         # 浅拷贝
```

dict常见方法:

```python
d.get(key)             # 安全取值（不存在返回None）
d.keys()               # 所有键
d.values()             # 所有值
d.items()              # 键值对

d.update(other)        # 更新字典
d.setdefault(k, v)     # 不存在则设置

d.pop(key)             # 删除并返回
d.popitem()            # 删除最后一项
d.clear()              # 清空

d.copy()               # 浅拷贝
```

set常见方法:

```python
s.add(x)               # 添加元素
s.update(iter)         # 添加多个

s.remove(x)            # 删除（不存在会报错）
s.discard(x)           # 删除（不存在不报错）
s.pop()                # 随机删除一个

s.clear()              # 清空
s.copy()               # 浅拷贝

s1 | s2    # 并集
s1 & s2    # 交集
s1 - s2    # 差集
s1 ^ s2    # 对称差集
```

tuple常见方法:

```python
t.count(x)     # 统计次数
t.index(x)     # 查找索引
```

# 字符串编码和解码

为什么要编码和解码? 因为将字符串输入计算机时, 计算机需要识别字节, 通过传输字节到另一台计算机, 再解码变成字符串输入.

如何编码和解码? 其实就是两个方法: 字符串的encode()方法, 字节类型的decode()方法.

## 格式字符串

占位符, f-string, str.format()这三种方法均能使字符串格式化. 

个人最喜欢使用f-string:

```python
name = 'L'
age = 18
print(f"名字: {name}, 年龄: {age}")
```

# 正则表达式

元字符有哪些? 

- .: 匹配热议字符(除\n)
- \w: 匹配字母, 数字, 下划线
- \W: 匹配非字母, 数字, 下划线
- \s: 匹配任意空白字符
- \S: 匹配任意非空白字符
- \d: 匹配任意十进制数

限定符有哪些? 用来限定次数的

- ?: 0次或1次
- +: 1次或多次
- *: 0次或多次
- {n}: n次
- {n,}: 最少n次
- {n, m}: 最少n次, 最多m次

如何使用呢? 要用到re模块: 

```python
re.match(pattern, string, flags = 0)
re.search(pattern, string, flags = 0)
re.findall(pattern, string, flags = 0)
re.sub(pattern, string, count, flags = 0)
re.split(pattern, string, maxsplit, flags = 0)
```

# 今日总结

今日所学内容: if...elif...else, match, for, while, break, continue, pass, 列表, 元组, 字典, 集合, 字符串, 正则表达式. 