---
title: HTML基础标签介绍
url: 1432.html
id: 1432
categories:
  - HTML&amp;CSS
  - 文章页
date: 2018-07-08 19:32:43
tags:
  - HTML
  - CSS
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180708191725.png)

**基础标签介绍**

在HTML中标签都是成对出现的，开始为<标签>结束为</标签> 首先介绍一下<html>,这个标签是告诉浏览器这是一个html文件，有了这个标签浏览器才能识别HTML文件。 <head>是用来设置浏览器头信息的标签，包括浏览器的标题。 <title>用来设置网页标题在<head>中完成 格式为：**<title>标题</title>** <body>中存储的是显示在浏览器中给用户看到的信息，同样这里可以同样式表来设置更加美观的界面。 <p>标签P是用来显示段落，在其中写出的内容会在浏览器界面中显示出来。 同样在标签body中还有六级标题标签从<h1>到<h6> 具体使用：
```
<!DOCTYPE html>
<html lang="en">
<!--head为页面的头，网页的信息放到这里面-->
<head>
    <meta charset="UTF-8">
    <!--使用title可以设置页面标题-->
    <title>Starbuzz Coffee</title>
    <!--使用样式表-->
    <!--需要注意样式表的注解和html的注解不一样-->
    <style type="text/css">
        body
        {
            /*背景颜色*/
            background-color: #dd1144;
            /*设置左右外边距分别为20%*/
            margin-left: 20%;
            margin-right: 20%;
            /*定义界面主体周边的边框为虚线，颜色为黑色*/
            border: 2px dotted green;
            /*设置页面主体周围的内边距*/
            padding: 10px 10px 10px 10px;
            /*设置主体字体*/
            font-family: sans-serif;
        }
    </style>
</head>
<!--body为主体包含页面内容等，它是你在浏览器里面看到的内容，大多数空白符、制表符、换行符都会被忽略-->
<body>
<!--h1到h6表示页面标题-->
<h1>Starbuzz Coffee Beverages</h1>

<h2>House Blend,$1.49</h2>
<!--p标签用于显示段落-->
<p>A smooth,mild blend of coffees from Mexico,Bolivia and Guatemala.</p>

<h2>Mocha Cafe Latte,$2.35</h2>
<p>Espresso,steamed milk and chocolate syrup.</p>

<h2>Cappuccino,$1.89</h2>
<p>A mixture of espresso,steamed millk and foam</p>

<h2>Chai Tea,$1.85</h2>
<p>A spicy drink made with black tea,spices,milk and honey</p>
</body>
</html>

这是还要说一下HTML页面中使用<!--注释内容-->用来添加一些注释，添加注释是一个好习惯，增强代码的可阅读性。 再说一下标签<style>是用来设置样式表的。格式为：**<style type="">** 这里其实可以写好样式表文件，然后在该标签中引用即可。   下面介绍一下标签a 标签a可以用来引用一些HTML页面 使用格式为：**<a href="example.html">** 同样除了引用html页面也可以直接引用一些网址。 具体使用：

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Strudy the use of <a></title>
</head>
<body>
<h1>The introduction of the DongMan</h1>
<!--引用图片-->
<!--html里面的换行符为<br />-->
<img src="qwe.jpg">
<p>
    This is the picture of a katong girl<br />
    <!--使用a标签可以在在href后面加上一个url连接或者直接引用一个html页面，<a>这个内容是显示在html界面上的点击之后会跳转到指定的界面</a>-->
    learning more <a href="https://www.baidu.com/">hello</a>
</p>
<h2>test</h2>
<p>
    Nothing is something
    <a href="example 1.html">exits</a>
</p>
</body>
</html>
```
同样还可以使用**<img src="">**来引用一些图片，同样可以为本地图片也可以为图片的地址。