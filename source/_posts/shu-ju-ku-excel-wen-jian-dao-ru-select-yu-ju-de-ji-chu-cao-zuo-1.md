---
title: 数据库 Excel文件导入&Select语句的基础操作
url: 724.html
id: 724
categories:
  - 数据库
  - 文章页
date: 2018-05-01 13:12:12
tags:
  - SQL
  - DataBase
  - Excel
---

![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180412181315.png) 通过使用SQL Sever 导入excel表格数据： 步骤： 1.通过任务选项中的导入数据进行导入 ![](http://47.100.4.8/wp-content/uploads/2018/05/321.png) 2.选择你想要导入的数据： ![](http://47.100.4.8/wp-content/uploads/2018/05/3212.png) 3.选择你本地的数据库 并输入需要的输入的数据 ![](http://47.100.4.8/wp-content/uploads/2018/05/32123.png) 4.选择对应表进行数据导入： ![](http://47.100.4.8/wp-content/uploads/2018/05/13241.png) 这里需要注意的是左侧一栏为源文件可导入的表，右侧一栏是导入你自己创建表中。 5.之后就一直下一步即可创建成功。 ![](http://47.100.4.8/wp-content/uploads/2018/05/852.png) 需要注意的是：在导入数据之前要记得先创建文件中对应的表以及数据要求 还有一点需要注意的是：如果在导入excel文件时弹出如下提示框： ![](http://47.100.4.8/wp-content/uploads/2018/05/9636.png) 那么你需要去Microsoft 官网上下载对应你office版本号的Microsoft office access database engine 2016 比如我这里就是2016版本的。   select语句的使用：

*   查询计算机系的学生信息

代码：
```
select * from S$   （*号的作用是显示所有内容）

where SDEPT='计算机'

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/1.png)

*   between语句配合select的使用：

代码：

select * from S$

where SAGE between 19 and 21

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/2.png)

*   符号表达式的使用：
```
代码：
```
select * from S$

where SAGE<20 and SSEX='女'

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/3.png)

*   %的使用：
```
代码：
```
select * from S$

where SNAME like '%伟'  （目的是显示所有以伟结果的名称）

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/4.png)

*   like 是用于字符串 的匹配
```
代码：
```
select * from C$

where CNAME like '数据库' or CNAME like'操作系统' or CNAME like'数据库实验'

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/5.png)

*   = 用于数值的比较
```
代码：
```
select SNO from SC$

where CNO = 2

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/6.png)

*   max（） min（）  avg（） 的使用：
```
代码：
```
select '最高分'=MAX(GRADE),'最低分'=MIN(GRADE),'平均分'=AVG(GRADE)

from S,C,SC

where S.SNO=SC.SNO and C.CNO=SC.CNO and CNAME like '操作系统'

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/7.png)

*   top语句的使用：
```
代码：
```
select  top 3 S.*,GRADE  （选择出成绩前三名）

from S,C,SC

where S.SNO=SC.SNO and C.CNO=SC.CNO and C.CNAME = '操作系统'

order by GRADE DESC  （梯度下降）
```
    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/8.png)