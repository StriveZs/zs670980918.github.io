---
title: Python isinstance() 函数
url: 1269.html
id: 1269
categories:
  - Python知识
  - 文章页
date: 2018-05-27 13:09:44
tags:
  - Python
---

![](http://47.100.4.8/wp-content/uploads/2018/05/u407244128253124607fm27gp0.jpg) **描述** isinstance() 函数来判断一个对象是否是一个已知的类型，类似 type()。 _isinstance()_ _与_ _type()_ _区别：_

*   _type()_ _不会认为子类是一种父类类型，不考虑继承关系。_
*   _isinstance()_ _会认为子类是一种父类类型，考虑继承关系。_

_如果要判断两个类型是否相同推荐使用_ _isinstance()__。_ **语法** 以下是 isinstance() 方法的语法: isinstance(object, classinfo) **参数**

*   object -- 实例对象。
*   classinfo -- 可以是直接或间接类名、基本类型或者有它们组成的元组。

**返回值** 如果对象的类型与参数二的类型（classinfo）相同则返回 True，否则返回 False。。 **实例** 以下展示了使用 isinstance 函数的实例：
``
a=2
print(isinstance(a,int))
print(isinstance(a,str))
``
结果 第一个返回True 第二个返回False **type()** **与** **isinstance()****区别：**
```
class A: pass class B(A):

     pass isinstance(A(), A) 

type(A()) == A 

isinstance(B(), A)
```
结果： 第一个返回True 第二个返回False 第三个返回True   本文参考了python菜鸟教程中的文章，感谢该博主提供的知识。