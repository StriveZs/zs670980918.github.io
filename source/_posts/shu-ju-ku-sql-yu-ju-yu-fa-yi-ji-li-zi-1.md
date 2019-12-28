---
title: 数据库SQL语句语法以及例子
url: 1371.html
id: 1371
categories:
  - 数据库
  - 文章页
  - 语法与例题
date: 2018-06-21 23:19:42
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180621230739.png) **select****语句的使用：** SELECT 列名称 FROM 表名称 下面例题使用到的数据表为：[SC](http://47.100.4.8/wp-content/uploads/2018/06/SC.xlsx)

*   查询计算机系的学生信息

代码：

select *

from S

where SDEPT='计算机'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/1.png)

*   查询年龄在19至21【包含19至21】之间的学生信息

代码：  

select *

from S

where SAGE between 19 and 21

截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/2.png)

*   查询20岁以下的女生信息

代码：

select *

from S

where SAGE<20 and SSEX='女'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/3.png)

*   查询姓名中最后一个字是“伟”的学生信息

代码：

select *

from S

where SNAME='%伟'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/4.png)

*   查询学号以“E”开头的学生信息

代码：

select *

from S

where SNO like 'E%'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/5.png)

*   查询“数据库”、“操作系统”、“数据库实验”课程的信息

代码：

select * from C

where CNAME = '数据库' or CNAME ='操作系统' or CNAME ='数据库实验'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/6.png)

*   查询2号课程的选修情况

代码：

select *

from SC

where CNO=2

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/7.png)

*   查询某个学生的选课情况（学生学号自定）

代码：

select SNO,CNO

from SC

where SNO='A0001'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/9.png)

*   查询成绩90分以上的选课情况

代码：

select SNO,CNO

from SC

where GRADE > 90

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/10.png)

*   查询所有选课中的2个最高分

代码：

select top 2 GRADE,SNO  --注意在top前面不能添加语句

from SC

order by GRADE desc

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/11.png)