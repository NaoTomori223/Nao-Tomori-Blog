# 文件及IO操作

## 文件流程操作

基本写法: 打开文件 --> 操作文件 --> 关闭文件

打开文件: 变量名 = open(filename, mode, encoding)

操作文件(读/写): 变量名.read()/变量名.write(str)

关闭文件: 变量名.close()

进阶写法: with open(filename, mode, encoding) as file: pass

**文件打开模式:** 

- r: 以只读模式打开, 文件指针在文件的开头, 如果文件不存在, 程序抛异常.

- rb: 以只读模式打开二进制文件, 如图片文件.

- w: 覆盖写模式, 文件不存在创建, 文件存在则内容覆盖.

- wb: 覆盖写模式写入二进制数据, 文件不存在则创建, 文件存在则覆盖.

- a: 追加写模式, 文件不存在创建, 文件存在, 则在文件最后追加内容.

- +: 与w/r/a等一同使用, 在原功能的基础上增加同时读写功能.

**文件读写方法:**

- file.read(size): 从文件中拂去size个字符或字节, 如果没有给定参数, 则读取文件中全部内容.

- file.readline(size): 读取文件中的一行数据, 如果给定参数, 则为读取这一行中的size个字符或字节.

- file.readlines(): 从文件中读取所有内容, 结果为列表类型.

- file.write(s): 将字符串s先写入文件.

- file.writelines(lst): 将内容全部为字符串的列表lst写入文件.

- file.seek(offset): 改变当前文件操作指针的位置, 英文占一个字节, 中文gbk编码占两个字节, utf-8编码占三个字节.

**os模块常用方法:**

- python内置的与操作系统文件相关的模块.

- getcwd(): 获取当前工作路径.

- listdir(path): 获取path路径下的文件和目录信息, 如果没有指定path, 则获取当前路径下的文件和目录信息.

- mkdir(path): 在指定路径下创建目录(文件夹).

- makedirs(path): 创建多级目录.

- rmdir(path): 删除path下的目录.

- removedirs(path): 删除多级目录.

- chdir(path): 把path设置为当前目录.

- walk(path): 遍历目录树, 结果为元组, 包含所有路径名, 所有目录列表和文件列表.

- remove(path): 删除path指定的文件.

- rename(old, new): 将old重命名为为new.

- stat(path): 获取path指定的文件信息, 大部分信息都是时间戳, 需要转换.

- startfile(path): 启动path指定文件.

**os.path模块常用方法:**

- abspath(path): 获取目录或文件的绝对路径.

- exists(path): 判断目录或文件在磁盘上是否存在, 结果为bool类型. 存在为True, 否则为False.

- join(path, name): 将目录与目录名或文件名进行拼接, 相当于字符串的'+'操作.

- splitext(): 分别获取文件名和后缀名.

- basename(path): 从path中提取文件名.

- dirname(path): 从path中提取路径(不包含文件名).

- isdir(path): 判断path是否是有效路径.

- isfile(path): 判断file是否是有效文件.

## 数据的组织维度及存储

**一维数据:** 

通常采用线性方式组织数据, 一般用列表, 元组或集合进行存储数据.

**二维数据:** 

也称表格数据, 类似于Excel表格, 用二维列表进行存储.

**高维数据:** 

用key-value的方式进行组织数据, 用字典存储数据. Python中内置的json模块专门用于处理JSON(JavaScript Object Notation)格式的数据.

**json模块常用函数:**

- json.dumps(obj): 将python数据类型转成JSON格式, 编码过程.

- json.loads(s): 将JSON格式字符串转成python数据类型, 解码过程.

- json.dump(obj, file): 与dumps()功能相同, 将转换结果存储到文件file中.

- json.load(file): 与loads()功能相同, 从文件file中读入数据.

## 实战: 记录用户登录日志并查看

```python
def log_in():
    username = input('请输入用户名: ')
    password = input('请输入密码: ')
    with open('用户信息.txt', 'r') as file:
        lst = file.readline().split(' ')
        lst[1] = lst[1][:len(lst[1]) - 1]
        if username == lst[0] and password == lst[1]:
            local_time = time.time()
            with open('用户登录日志.txt', 'a') as f:
                f.write(date_format(local_time))
                f.write('\n')
            check()

def make_user():
    print('----------开始注册账号----------')
    username = input('请输入用户名: ')
    password = input('请输入密码: ')
    with open('用户信息.txt', 'a') as file:
        file.write(' '.join([username, password]))
        file.write('\n')

def check():
    with open('用户登录日志.txt', 'r') as file:
        print('----------登录日志----------')
        print(file.read())

def date_format(struct_time):
    local_time = time.localtime(struct_time)
    s = time.strftime('%Y-%m-%d %H:%M:%S', local_time)
    return s

if __name__ == '__main__':
    try:
        choice = input('你是否有账号? (y/n): ')
        if choice == 'y':
            log_in()
        elif choice == 'n':
            make_user()
        else:
            raise Exception('请输入正确指令!')
    except Exception as e:
        print(e)
```

**debug找到问题:**

![](/blogs/python-basis-4/eed56d7dec1915d1.png)

我是想用用户输入的密码与用户信息这个文件里的该用户正确密码进行比较, 如果正确则登录成功, 执行下面的代码.

起初在写入用户信息的时候, 因为考虑到美观所以加入换行符'\n', 然后通过debug发现了这个原因导致无法执行下面代码.

**如何解决?**

要想对比密码, 肯定要把换行符'\n'删除, 所以我就用了**字符串的切片**, 把'\n'前面的字符串都获取出来, 然后就可以与用户输入的密码进行比较.

会debug是个很加分很有用的技能.

# 网络编程

**通信协议:**

协议就是规则, 通信协议的作用是让全世界不同的计算机都可以连接起来, 形成护理网

## TCP/IP协议

**IP协议:**

是整个TCP/IP协议族的核心. IP地址(IPv4, IPv6)就是互联网上计算机的唯一标识.

**TCP协议:**

TCP(**T**ransmission **C**ontrol **P**rotocol)协议即传输控制协议, TCP协议负责两台计算机之间建立可靠连接, 保证数据包按顺序发送. 它是一种**可靠的**, **一对一的**, **面向有连接的**通信协议. 

**TCP三次握手确立连接:**

![](/blogs/python-basis-4/fb8d098748efb1b7.png)

## UDP协议

UDP协议又称用户数据包协议(**U**ser **D**atagram **P**rotocol), 它是**面向无连接的**协议, 只要知道对方的IP地址和端口, 就可以直接发送数据包, 由于是面向无连接的, 所以**无法保证数据一定会到达接收方.**

什么是端口号? 区分计算机中**运行的应用程序**的整数. 端口号取值范围是0-65535, 其中80这个端口号分配给了HTTP服务, 21这个端口号给了FTP服务.

**TCP协议和UDP协议的区别:**

![](/blogs/python-basis-4/1616c2f85b8f57a6.png)

## Socket

是什么? 用来描述IP地址和端口号的.

**socket对象常用方法:**

- bind((ip, port)): 绑定IP地址和端口.

- listen(N): 开始TCP监听, N表示操作系统挂起的最大连接数量, 取值范围1-5, 一般设置为5.

- accept(): 被动接收TCP客户端连接, 阻塞式.

- connect((ip, port)): 主动初始化TCP服务器连接.

- recv(size): 接收TCP数据, 返回值为字符串类型, size表示要接受的最大数据量.

- send(str): 发送TCP数据, 返回值是要发送的字节数量.

- sendall(str): 完整发送TCP数据, 将str中的数据发送到连接的套接字, 返回之前尝试发送所有数据, 如果成功为None, 失败抛出异常.

- recvfrom():接收UDP数据, 返回值为一个元组(data, address), data表示接收的数据, address表示发送数据的套接字地址.

- sendto(data, (ip, port)): 发送UDP数据, 返回值是发送的字节数.

- close(): 关闭套接字.

## 实现TCP的多次通信

**首先要创建服务器端:**

```python
import socket

# (1) 创建socket对象
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# (2) 绑定ip地址和端口号
server_socket.bind(('127.0.0.1', 8888)) # 端口号统一为 8888

# (3) 使用listen()开始监听
server_socket.listen(5)
print('服务器已经启动，等待客户端连接...')

# (4) 等待客户端的连接
client_socket, client_addr = server_socket.accept()
print(f'与客户端 {client_addr} 连接成功！')

# (5) 接收客户端发送的数据
info = client_socket.recv(1024).decode('utf-8') # 使用 client_socket 接收
while info != 'bye':
    if info != '':
        print('客户端发来的数据为: ', info)
    # 准备发送数据
    data = input("输入想要发送的数据: ")
    client_socket.send(data.encode('utf-8'))

    if data == 'bye': # 判断发送的是否为 'bye'
        break

    # 继续使用client_socket接收数据
    info = client_socket.recv(1024).decode('utf-8')

print('客户端已退出')

# (6) 关闭连接
client_socket.close()
server_socket.close()
```

**还需要一个客户端:**

```python
import socket

# (1) 创建socket对象
client_socket = socket.socket()

# (2) 连接服务器
client_socket.connect(('127.0.0.1', 8888))  # 端口号统一为 8888
print('----------与服务器连接建立成功----------')

# (3) 发送和接收数据
info = ''
while info != 'bye':
    # 准备发送数据
    info = input('输入想要发送的数据: ')  # 将输入赋值给 info
    client_socket.send(info.encode('utf-8'))

    if info == 'bye':
        break

    # 接收一条数据
    data = client_socket.recv(1024).decode('utf-8')
    print('收到服务器端的数据: ', data)

# (4) 关闭客户端
client_socket.close()
```

实现多次通信的关键就是while循环. **注意: 开始通信时, 要先运行服务器端, 再运行客户端.**

## 实现UDP的一次双向通信

**首先需要一个发送方:**

```python
import socket

# 实现UDP编程(发送方):
# (1) 创建socket对象
sender_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# (2) 准备发送数据
data = input('请输入要发送的数据: ')

# (3) 指定接收方的IP地址和端口
ip_port = ('127.0.0.1', 8888)

# (4) 发送数据
sender_socket.sendto(data.encode('utf-8'), ip_port)

# 接收来自接收方的回复数据
recv_data, recv_addr = sender_socket.recvfrom(1024)
print('接收方的数据为: ', recv_data.decode('utf-8'))

# (5) 关闭socket对象
sender_socket.close()
```

**还需要一个接收方:**

```python
import socket

# 实现接收方

# (1) 创建socket对象
recver_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# (2) 绑定IP地址和端口
recver_socket.bind(('127.0.0.1', 8888))

# (3) 接收来自发送方的数据
recv_data, addr = recver_socket.recvfrom(1024)
print('接收到的数据为: ', recv_data.decode('utf-8'))

# (4) 准备回复对方的数据
data = input("请输入要回复的数据: ")

# (5) 回复
recver_socket.sendto(data.encode('utf-8'), addr)

# (6) 关闭
recver_socket.close()
```

**注意: 运行程序时, 需要先运行接收方程序, 再运行发送方程序.**

# 总结

今日学习内容: 文件操作, os模块, os.path模块还有数据的组织维度及存储, TCP/IP协议, UDP协议, Socket模块, TCP编程和UDP编程.