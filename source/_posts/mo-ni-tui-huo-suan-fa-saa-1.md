---
title: 模拟退火算法（SAA）
url: 427.html
id: 427
categories:
  - 文章页
  - 算法
date: 2018-03-24 13:52:39
tags:
  - Algorithm
  - SA
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180324133549-222x300.png)

### 简介：

### 模拟退火算法**是一种通用概率演算法，用来在一个大的搜寻空间内找寻命题的最优解。**它是基于Monte-Carlo迭代求解策略的一种随机寻优算法。**模拟退火算法是解决TSP问题的有效方法之一。**

模拟退火算法来源于固体退火原理。 固体退火：将固体加温至充分高，再让其徐徐冷却，加温时，固体内部粒子随[温升](https://baike.baidu.com/item/%E6%B8%A9%E5%8D%87)变为无序状，内能增大，而徐徐冷却时粒子渐趋有序，在每个温度都达到平衡态，最后在常温时达到基态，内能减为最小。 ——百度百科 为了介绍模拟退火算法就必须为大家介绍一下爬山算法，简单地说模拟退火算法是在该算法上的改进。 ![](http://47.100.4.8/wp-content/uploads/2018/03/u25054793203405929506fm27gp0-300x97.jpg) 这里的爬山算法就是一种简单的贪心算法，它又可以成为局部搜索算法，如上图所显示的，当它处于C点时，他回去寻找临近空间的最优解即为A点，但是当它找到A点时后，就不会在继续往下去搜索了，这就导致了在搜索过程陷入局部最优解中而出不来以至于找不到最优解。 相遇比较与非常贪心的爬山算法，模拟退火算法，则是一种全局搜索算法（它也是一种贪心算法）全局的意义在于：它在到达局部最优解时，会有一定的概率继续向右移动，以上图为例：当到达局部最优解A后会有一定的概率继续到达E点然后继续向右搜索，这样的过程就有可能会找到全局最优解B了。 关于上面提到的一定的概率解释如下： 如果：F（t+1）<=F(t)即为移动后会有更优解，那么下次移动就一定会被接收 如果：F(t+1)>F(t) 即为可能移动后的解比当前的解要差，则只能以一定的概率接收而这样的概率会逐渐减弱。这样的减弱取决于衰弱值a。当然减弱也要有一定的限度，即为最后趋于稳定的值。 下面是它的伪代码： ![](http://47.100.4.8/wp-content/uploads/2018/03/行政村自行车-300x190.png)   这就是模拟退火算法的主要思想介绍。 以上内容一部分参考了网络上别人的一些博文。