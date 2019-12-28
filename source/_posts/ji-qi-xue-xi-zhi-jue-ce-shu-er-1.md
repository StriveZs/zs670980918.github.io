---
title: 机器学习之决策树（二）
url: 591.html
id: 591
categories:
  - 决策树
  - 文章页
  - 机器学习
date: 2018-04-15 12:57:18
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg)   这里使用ID3算法划分数据集。 ID3算法的伪代码： ID3（例子，目标属性，属性） 为树创建一个根节点 如果所有示例都是肯定的，则返回单节点树Root，其中label = +。 如果所有示例均为负数，则返回单节点树Root，标签为 - 。 如果预测属性的数量为空，则返回单节点树Root， 标签=示例中目标属性的最常见值。 否则开始 A←最佳分类示例的属性。 Root = A的决策树属性 对于A的每个可能的值_v __i_， 在Root下添加一个新的树分支，对应于测试A = _v __i_。 让例子（_v __i_）成为A 的值为_v __i_的例子的子集 如果示例（_v __i_）为空 然后在这个新分支下面添加一个标签=最常见目标值的叶节点 否则，在这个新分支下面添加子树ID3（Examples（_v __i_），Target_Attribute，Attributes  -  {A}） 结束 返回根 ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180415125137.png) 划分数据集的大原则：将无序的数据变得更加有序。 在划分数据集之前之后信息发生的变化称为信息增益。对于特征值的选择当前是信息增益最高的特征值是最好的特征值。 熵定义为：信息的期望值。 计算给定数据集的熵：

import math
import operator

#计算给定数据集的熵
def calcShannonEnt(dataSet):
    numEntries = len(dataSet) #得到数据集中数据的个数
    #为所有可能分类创建字典
    labelCounts = {} #创建一个空的字典
    for featVec in dataSet: #遍历每一个数据
        currentLabel = featVec\[-1\] #得到该数据最后一列的值作为键值
        if currentLabel not in labelCounts.keys(): #如果该键值不在已有的字典键值中
            labelCounts\[currentLabel\] = 0 #则拓展字典并将当前键值加入字典
        labelCounts\[currentLabel\] += 1 #记录每个键值出现的次数
    shannonEnt = 0.0 #初始化概率
    for key in labelCounts: #遍历字典中的键值
        prob = float(labelCounts\[key\]) / numEntries #计算初步该键值出现次数所占的概率
        shannonEnt -= prob * math.log(prob,2) #用上面的概率计算本次的熵
    return shannonEnt #返回最终熵

  简单的应用： 先创建一个简单的数据 在以后的实验中会使用大量的数据这里自己先构建一个简单的： ![](http://47.100.4.8/wp-content/uploads/2018/04/23232323.png) 使用： ![](http://47.100.4.8/wp-content/uploads/2018/04/323232323.png) 结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/34234234234.png)![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180416221958.png) 熵越高，则混合的数据也越多。 计算熵的值也是为了以后找到最优划分数据集做准备。   选择最好的数据集划分方式： ![](http://47.100.4.8/wp-content/uploads/2018/04/4334234234.png)

#选择最好的数据集划分方式
def chooseBestFeatureToSplit(dataSet):
    #函数调用的要求是：数据必须是一种由列表元素组成的列表，而且所有的列表元素都要具有相同的数据长度
    #数据的最后一列或者每个实例的最后一个元素是当前实例的类别标签
    numFeatures = len(dataSet\[0\]) - 1 #这里操作的目的是 得到\[\[0,1,2,3\],\[0,1,2,3\]\] 四列-1  得到子列表中除标签之外的特征值的总列数 
    baseEntropy = calcShannonEnt(dataSet)  #计算整个数据集的熵
    bestInfoGain = 0.0  #初始化最好信息收益
    bestFeature = -1  #初始化最好信息收入的对应特征值的在数据集中的位置 \[\[0,1,2\]\]  若返回0 则代表第0个特征值是用来划分数据集最好的特征
    #创建唯一的分类标签
    for i in range(numFeatures): 
        featList = \[example\[i\] for example in dataSet\] #访问每个列表的子列表 中的除标签之外的在同一位置上的特征值并将它们组成一个新的列表
        uniqueVals = set(featList) #这里使用set（）创建该列表特征值的无序不重复的集合 这里得到的是每一个子列表对应列上的特征值的不重复无序集合
        #计算按照第i列特征值划分的数据集的信息熵
        newEntropy = 0.0 #初始化
        for value in uniqueVals: #遍历上面创建的无序不重复特征值集合  目的是得到分别按照在该列上不同的特征值所划分得到的数据集，并且计算该种划分的熵
            subDataSet = splitDataSet(dataSet,i,value)  #得到该数据集对于该特征值的划分
            prob = len(subDataSet)/float(len(dataSet))  #计算该数据集划分方式在原数据集中的所占比
            newEntropy += prob * calcShannonEnt(subDataSet)  #得到新的信息增益 = 所占比*数据集新划分方式的熵
        #计算最好的信息收入
        infoGain = baseEntropy - newEntropy
        if(infoGain > bestInfoGain): #如果numfaetures大于1 则进行多列特征值都进行划分  得到数据依次在这里比较 保留下最好的
            bestInfoGain = infoGain  #获得最好的信息收入
            bestFeature = i  #得到最好信息收入位置对应特征值的位置
    return bestFeature  #返回的是按照第几列划分得到的数据集最好  也可以你看成找到树上的一个结点

  举例解释： ![](http://47.100.4.8/wp-content/uploads/2018/04/32112313.png)![](http://47.100.4.8/wp-content/uploads/2018/04/9636363.png) 对于这个列表会先遍历第一列所有元素\[1,1,1,0,0,0\] 是在代码的48行到57行实现的 通过set（） 会得到不重复无序的列表\[1,0\]或者\[0,1\]  是在代码得58行实现的 然后依次根据其中每一个特征值以及列标 进行划分在代码的62行实现的 剩下的就是进行数据之间操作 为的是进行最优解的选择 63行到70行 ps：遍历完这一列会进行下一列\[1,1,0,1,1,1\]的遍历重复上面操作，如果有更多列则继续进行。   End！