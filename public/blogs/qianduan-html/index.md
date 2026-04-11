# 什么是HTML

**HTML**: **H**yper**T**ext **M**arkup **L**anguage, 超文本标记语言.

**超文本**：超越了文本的限制, 比普通文本更强大. 除了文字信息, 还可以定义图片、音频、视频等内容.

**标记语言**：由标签 "<标签名>" 构成的语言. HTML标签都是预定义好的, 直接使用即可. HTML代码直接在浏览器中运行，HTML标签由浏览器解析. 

万维网联盟(W3C)推荐HTML使用小写, 浏览器解析部分大小写.

# HTML基本结构

Web浏览器读取HTML文档, 并以网页的形式显示出它们. 浏览器不会显示HTML标签, 而是使用标签来解释页面的内容, 以下是HTML固定的基本结构:

- **\<html\>**: 定义整个网页. 

- **\<head>**: 定义网页的头部, 用来存放给浏览器看的信息, 如: CSS样式、网页的标题.

- **\<body\>**: 定义网页的主体部分, 存放给用户看的信息, 也是网页的主体内容, 如: 文字、图片、视频、音频、表格等.

  HTML基本结构如下: 

```html
<html>
     <head>
          <title>HTML 固定基本结构</title>
     </head>
     <body>
          <h1>Hello HTML</h1>
          <img src="img/1.png">
     </body>
</html>
```

# HTML常见标签

HTML常见标签

- **\<h1\>......\<h6\>**: h1为一级标题，字体也是最大的; h6为六级标题, 字体是最小的.
- **\<a\>**: 超链接标签. 属性href: 指定资源访问的url; 属性target: 指定在何处打开资源链接, _self: 默认值, 在当前页面打开, _blank: 在空白页面打开.
- **\<video\>**: 视频标签. 属性: src: 指定视频的url; control: 是否显示播放控件; width: 宽度(单位: 像素px或者相对父元素的百分比); height: 高度(单位: 像素px或者相对父元素的百分比). width 和height一般只写一个, 另一个会等比例放缩.
- **\<img\>**: 图片标签. 属性: src, width, height.
- **\<p\>**: 段落标签.
- **\<br /\>**: 换行标签.
- **\<hr /\>**: 水平线标签.
- **\<b\> / \<strong\>**: 加粗, \<strong\> 具有强调意义.
- **\<u\> / \<ins\>**: 下划线, \<ins\> 具有强调意义.
- **\<i\> / \<em\>**: 倾斜, \<em\> 具有强调意义
- **\<s\> / \<del\>**: 删除线, \<del\> 具有强调意义
- **\<div\>**: 布局标签, 没有语义. 一行只显示一个(独占一行). 宽度默认是父元素的宽度, 高度默认由内容撑开. 可以设置宽高(width、height).
- **\<span\>**: 布局标签, 没有语义. 一行可以显示多个. 宽度和高度默认由内容撑开. 不可以设置宽高(width、height).
- **\<form\>**: 表单标签. 属性: action: 规定表单提交时, 向何处发送表单数据, 表单提交的url; method: get: 表单数据是拼接在url后面的, 如: xxxxxxxxxxx?username=Tom&age=12, url中能携带的表单数据大小是有限制的. post: 表单数据是在请求体(消息体)中携带的, 大小没有限制.
- **\<input\>**: 定义表单项, 通过type属性控制输入形式. (type为button时是纯按钮, 可结合JavaScript实现功能).

![](/blogs/qianduan-html/53be2e598b7c1115.png)

- **\<select\>**: 定义下拉列表, \<option\>定义列表项.
- **\<textarea\>**: 定义文本域.
- **\<table\>**: 定义表格整体.
- **\<thead\>**: 定义表格头部.
- **\<tbody\>**: 定义表格中的主体部分.
- **\<tr\>**: 表格的行, 可以包裹多个\<td\>.
- **\<td\>**: 表格单元格(普通), 可包含内容; 如果是表头单元格, 可换为\<th\>.

HTML标签手册: https://www.w3school.com.cn/tags/index.asp

# 表单标签应用举例

代码如下:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML-表单项标签</title>
</head>
<body>

<!-- value: 表单项提交的值 -->
<form action="/save" method="post">
     姓名: <input type="text" name="name"> <br><br>

     密码: <input type="password" name="password"> <br><br> 

     性别: <input type="radio" name="gender" value="1"> 男
          <label><input type="radio" name="gender" value="2"> 女 </label> <br><br>
     
     爱好: <label><input type="checkbox" name="hobby" value="java"> java </label>
          <label><input type="checkbox" name="hobby" value="game"> game </label>
          <label><input type="checkbox" name="hobby" value="sing"> sing </label> <br><br>
     
     图像: <input type="file" name="image">  <br><br>

     生日: <input type="date" name="birthday"> <br><br>

     时间: <input type="time" name="time"> <br><br>

     日期时间: <input type="datetime-local" name="datetime"> <br><br>

     学历: <select name="degree">
               <option value="">----------- 请选择 -----------</option>
               <option value="1">大专</option>
               <option value="2">本科</option>
               <option value="3">硕士</option>
               <option value="4">博士</option>
          </select>  <br><br>

     描述: <textarea name="description" cols="30" rows="10"></textarea>  <br><br>
     
     <input type="hidden" name="id" value="1">

     <!-- 表单常见按钮 -->
     <input type="button" value="按钮">
     <input type="reset" value="重置"> 
     <input type="submit" value="提交">   
     <br>
</form>

</body>
</html>
```

呈现结果:

![](/blogs/qianduan-html/aa35604c865d939e.png)

# 常见字符实体

- \&nbsp; --> 空格
- \&lt; --> <
- \&gt; --> >

# 绝对路径与相对路径

在引入图片、视频、音频、css等内容时, 我们需要指定文件的路径, 而在前端开发中, 路径的书写形式分为两类: 

1. 绝对路径:
   - 绝对磁盘路径: \<img src="C:\\Users\\Administrator\\Desktop\\HTML\\img\\logo.png"\>
   - 绝对网络路径: \<img src="gttps://i2.sinaimg.cn/dy/deco/2021/6013/yocc/cc20120613/img01/news_logo.png"\>
2. 绝对路径:
   - ./: 当前目录, ./可以省略
   - ../: 上一级目录