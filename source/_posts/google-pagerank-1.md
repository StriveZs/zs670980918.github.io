---
title: Google PageRank
url: 385.html
id: 385
categories:
  - Google —PageRank
  - 文章页
date: 2018-03-19 18:43:58
tags:
  - Google
  - PageRank
---

### ![](http://47.100.4.8/wp-content/uploads/2018/03/u24187857483070860104fm27gp0-300x216.jpg)

PageRank是一种比较经典的基于网页粒度的分析算法。他是谷歌搜索引擎的核心算法。简单的讲：他会根据网页之间的连接关系对网页的权重进行计算，并可以依靠这些计算出来的权重，对网页进行排名。

### 简介

         PageRank，网页排名，又称网页级别、Google左侧排名或佩奇排名，是一种由\[1\]  根据[网页](https://baike.baidu.com/item/%E7%BD%91%E9%A1%B5)之间相互的[超链接](https://baike.baidu.com/item/%E8%B6%85%E9%93%BE%E6%8E%A5)计算的技术，而作为网页排名的要素之一，以[Google](https://baike.baidu.com/item/Google)公司创办人[拉里·佩奇](https://baike.baidu.com/item/%E6%8B%89%E9%87%8C%C2%B7%E4%BD%A9%E5%A5%87)（Larry Page）之姓来命名。Google用它来体现网页的相关性和重要性，在[搜索引擎优化](https://baike.baidu.com/item/%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E%E4%BC%98%E5%8C%96/3132)操作中是经常被用来评估网页优化的成效因素之一。Google的创始人拉里·佩奇和[谢尔盖·布林](https://baike.baidu.com/item/%E8%B0%A2%E5%B0%94%E7%9B%96%C2%B7%E5%B8%83%E6%9E%97)于1998年在[斯坦福大学](https://baike.baidu.com/item/%E6%96%AF%E5%9D%A6%E7%A6%8F%E5%A4%A7%E5%AD%A6)发明了这项技术。

         PageRank通过网络浩瀚的超链接关系来确定一个页面的等级。Google把从A页面到B页面的链接解释为A页面给B页面投票，Google根据投票来源（甚至来源的来源，即链接到A页面的页面）和投票目标的等级来决定新的等级。简单的说，一个高等级的页面可以使其他低等级页面的等级提升。

                                                                                         ——来源百度百科

![](http://47.100.4.8/wp-content/uploads/2018/03/timg-3-300x162.jpg)

##### 算法原理：

PageRank的计算充分利用了两个假设：数量假设和质量假设。步骤如下： **1）在初始阶段：**网页通过链接关系构建起Web图，每个页面设置相同的PageRank值，通过若干轮的计算，会得到每个页面所获得的最终PageRank值。随着每一轮的计算进行，网页当前的PageRank值会不断得到更新。 **2）在一轮中更新页面PageRank得分的计算方法：**在一轮更新页面PageRank得分的计算中，每个页面将其当前的PageRank值平均分配到本页面包含的出链上，这样每个链接即获得了相应的权值。而每个页面将所有指向本页面的入链所传入的权值求和，即可得到新的PageRank得分。当每个页面都获得了更新后的PageRank值，就完成了一轮PageRank计算。

PageRank算法总的来说就是预先给每个网页一个PR值（下面用PR值指代PageRank值），由于PR值物理意义上为一个网页被访问概率，所以一般是1N，其中N为网页总数。另外，一般情况下，所有网页的PR值的总和为1。如果不为1的话也不是不行，最后算出来的不同网页之间PR值的大小关系仍然是正确的，只是不能直接地反映概率了。 预先给定PR值后，通过下面的算法不断迭代，直至达到平稳分布为止。 ![](http://47.100.4.8/wp-content/uploads/2018/03/20160816094700454-300x226.jpg)

##### 基本思想：

如果网页M存在一个指向网页B的连接，则表明T的所有者认为B比较重要，从而把T的一部分重要性得分赋予B。这个重要性得分值为：PR（M）/L(M) 其中PR（M）为M的PageRank值，L(M)为M的出链数 则B的PageRank值为一系列类似于T的页面重要性得分值的累加。 即一个页面的得票数由所有链向它的页面的重要性来决定，到一个页面的[超链接](http://zh.wikipedia.org/wiki/%E8%B6%85%E9%93%BE%E6%8E%A5 "超链接")相当于对该页投一票。一个页面的PageRank是由所有链向它的页面（链入页面）的重要性经过[递归](http://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92 "递归")算法得到的。一个有较多链入的页面会有较高的等级，相反如果一个页面没有任何链入页面，那么它没有等级。 ——以上参考了csdn上的一些博文。  

大家讲不如Google 讲 ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180317232716-300x162.png)

##### 来自Google的言论：

Chris：PageRank的命名是基于“Page”，还是和某个创始人有关？ Google：PageRank是以Google的联合创始人兼总裁Larry Page的名字命名的。 Chris：Google是否把PageRank视做显著区别于其它搜索引擎的一个特性？ Google：PageRank是一种能够使Google在搜索速度和搜索结果的相关性上区别于其它搜索引擎的技术。不唯如此，在排名公式中Google还使用了100种其它的算法。 Chris：Google是否认为引入PageRank可以显著提高搜索结果的质量？以后是否仍将继续使用PageRank？ Google：由于PageRank使用了量化方法来分析链接，所以它仍将是决定Google搜索结果页排名的一个重要因素。 Chris：您认为Google工具栏上的PageRank的信息对普通用户/网站管理员/搜索引擎优化专家来说各有什么意义？ Google：Google工具栏上所提供的PageRank信息仅作为一种网站评估信息使用。用户们会觉得它很有趣，网站管理员一般用它来衡量网站性能。不过，由于PageRank只是一个大体评估，所以对搜索引擎专家的价值并不大。 Chris：常有网站试图通过“链接工厂”和访客簿的手段达到提升PageRank的目的。对这样的网站Google有什么举措？ Google：Google的工程师会经常更新Google的排名算法以防止对Google排名的恶意操纵。

End！