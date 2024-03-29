---
title: 机器学习之决策树（一）
url: 585.html
id: 585
categories:
  - 决策树
  - 文章页
  - 机器学习
date: 2018-04-13 23:03:17
tags:
  - Machine Learning
  - Decision Tree
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) 我们经常使用决策树处理分类问题，近来的调查表明决策树也是最经常使用的数据挖掘算法。他十分的简单，甚至是你根本不需要了解机器学习的知识，就能搞明白决策树是如何工作的。 例如：一个假想的邮件分类系统 ![](http://47.100.4.8/wp-content/uploads/2018/04/32123123.png) 长方形代表判断模块，椭圆代表终止模块，表示已经得出结论，可以终止运行。从判断模块引出的左右箭头称作分支，他可以到达另一个判断模块或者终止模块。 决策树的优势：就在于数据形式非常容易理解。 优点：计算复杂度不高，输出结果易于理解，对中间值的缺失不敏感，可以处理不相关的特征数据。 缺点：可能会产生过度匹配问题。 使用数据类型：数值型和标称型。   在构造决策树时，我们需要解决的第一个问题是，当前数据集上哪个特征在划分数据分类时起决定性作用。为了找到决定性的特征，划分出最好的结果，我们必须评估每个特征。完成测试之后，原始数据集就被划分为几个数据子集。这些数据子集会分布在第一个决策点的所有分支上。如果某个分支下的数据属于同一类型，则当前无需阅读的垃圾邮件已经正确地划分数据分类，无需进一步对数据集进行分割。如果数据子集内的数据不属于同一类型，则需要重复划分数据子集的过程。划分数据子集的算法和划分原始数据集的方法相同，知道所有需要的相同类型的数据均在一个数据子集内。   创建分支的伪代码： createBranch（） 检测数据集中的每个子项是否属于同一分类： If so return 类标签 Else： 寻找划分数据集的最好特征 划分数据集 创建分支节点 for  每个划分的子集： 调用函数createBranch 并增加返回结果到分支节点中 return 分支节点 上面的伪代码函数是一个递归函数，接下来的博文中会陆续给出实际代码。 决策树的一般流程： （1）收集数据：可以使用任何方法。 （2）准备数据：树构造算法只适用于标称型数据，因此数值型数据必须离散化。 （3）分析数据：可以使用任何方法，构造树完成之后，我们应该检查图形是否符合预期。 （4）训练算法：构造树的数据结构。 （5）测试算法：使用经验树计算错误率。 （6）使用算法：此步骤可以适用于任何监督学习算法，而使用决策树可以更好地理解数据的内在含义。 这里就先初步了解一下决策树。理解它的实现办法以便于对后面博文中代码的的理解。ps：后面的代码我也是看了很久才弄得比较清楚。￣□￣｜｜ End！ ![](http://47.100.4.8/wp-content/uploads/2018/03/timg-1.jpg)