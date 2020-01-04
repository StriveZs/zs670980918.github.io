---
title: 数据库之视图操作
url: 1462.html
id: 1462
categories:
  - 数据库
  - 文章页
  - 语法与例题
date: 2018-07-23 15:58:16
tags:
  - DataBase
  - 视图操作
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180621230739.png)

*   建立计算机系学生视图CS_S ；

代码：
```
create view CS_S

as

select *

from S

where SDEPT = '计算机'

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/07/1-5.png)

*   建立计算机系女生视图CS_S1 ；

代码：

create view CS_S1

as

select *

from S

where SDEPT = '计算机' and SSEX = '女'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/2-3.png)

*   建立无先修课（Cpno为NULL）的课程视图NP_C；

代码：

create view NP_C

as

select *

from C

where CPNO is NULL

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/3-2.png)

*   建立计算机系选修1号课程的学生视图CS_S2 ；

代码：

create view CS_S2

as

select S.*

from S,SC

where S.SNO = SC.SNO and SC.CNO = '1'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/4-1.png)

*   建立计算机系选修数据库课程学生视图CS_S3 ；

代码：

create view CS_S#

as

select S.*

from S,SC,C

where S.SNO = SC.SNO and C.CNO = SC.CNO and C.CNAME = '数据库' and SDEPT = '计算机'

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/5-1.png)

*   将计算机系女生的年龄增加1岁；

代码：

update CS_S1

set SAGE = SAGE + 1

  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/6-1.png)

*   对CS_S3中学生专业修改为电子；

代码：

update CS_S3

set SDEPT = '电子'

where SNO = 'E0002'

  截图： 该学生被移出该视图了就 ![](http://47.100.4.8/wp-content/uploads/2018/07/7.png)

*   分别删除以上定义的各个视图。

代码：

drop view CS_S

drop view CS_S1

drop view CS_S2

drop view CS_S3

drop view NP_C
```
  截图： ![](http://47.100.4.8/wp-content/uploads/2018/07/8.png)