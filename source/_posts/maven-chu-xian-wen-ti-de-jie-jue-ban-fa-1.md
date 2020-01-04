---
title: maven出现问题的解决办法
url: 1567.html
id: 1567
categories:
  - Maven
  - SQLServer
  - Web
  - 文章页
date: 2018-10-14 12:51:46
tags:
  - maven
  - 问题解决
  - SQLServer
---

![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181014125017.png) 由于之前自己的SpringBoost出现了运行方面的问题，根据报错看出是maven.jar包管理上面的问题。因此这里总结了一下尝试过的方法。

1.  可以尝试project中clean来清除一下试试 
2.  如果出现SQLServerDirver报错lang.IllegalStateException: Cannot load driver class: com.microsoft.sqlserver.jdbc.SQLServerDri 可以先去看看application.properties中的spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=SuperMarket和spring.datasource.driver-class-name=com.microsoft.sqlserver.jdbc.SQLServerDriver是否出现书写错误，如果没有则看看是否有一些多余的空格没有删除
3.  如果上面方法仍然行不通，可以去看报错中那个文件包报错，在E:\\MavenReports\\mavenjar\\com删除出错的包，然后在xml中随便删除一个字符然后在添加回去，保存会自动下载对应的包，再次运行看看是否能正确运行。
4.  以上方法均是在保证代码书写正确时来进行操作的，如果代码方面有问题，可以看一下dao包、service包、Implement包和mapper文件中中函数名称是否对应，调用的参数是否对应等等都需要注意是否一致。还有就是注入的方法@Autowired是否书写 ，还有@Controller是否在Controller类中书写，以及在ServiceImpl实现类中是否输出@Service，最后就是确定接口文件和实现类是否创建正确。

上面的第三种方法 是我最后解决问题的办法，具体原因是因为maven出现了jar包缺少的问题。