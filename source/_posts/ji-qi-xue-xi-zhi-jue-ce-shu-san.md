---
title: 机器学习之决策树（三）
url: 600.html
id: 600
categories:
  - 决策树
  - 文章页
  - 机器学习
date: 2018-04-16 22:22:46
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) 创建一个投票表决器得到出现次数位的分类名称： ![](http://47.100.4.8/wp-content/uploads/2018/04/5446.png)

def majorityCnt(classList):  #类似一个投票表决代码 得到出现次数最多的分类名称也就是键值
    classCount = {}
    for vote in classList:
        if vote\[-1\] not in classCount.keys(): 
            classCount\[vote\[-1\]\] = 0
        classCount\[vote\[-1\]\] += 1
        #上面代码是计算出得到classList中每个键值出现的次数
    sortedClassCount = sorted(classCount.items(),key=operator.itemgetter(1),reverse=True) #进行字典排序
    return sortedClassCount\[0\]\[0\] #返回出现最多的分类名称  注意这里输出最大值的结果是按照ASCII吗排序靠前的就先输出了。 即使有两个出现次数一样多的也是按照谁排在前面就输出他

  工作原理：得到原始数据集，然后基于最好的属性值划分数据集，由于特征值可能多于两个，因此可能存在大于两个分支的数据集划分。在第一次划分之后，数据将被向下传递到树分支的下一个节点，在这个节点上，我们可以再次划分数据。因此可以采用递归构建决策树。 递归构建决策树： 递归结束的条件：程序遍历完所有划分数据集的属性，或者每个分支下的所有实例都具有相同的分支。   代码中的结束递归条件：

1.  所有标签类型相同，则直接返回该类标签。
2.  使用完了所有的特征值，仍然不能将数据集划分成仅包含唯一类别的分组。

这里递归调用的函数许多是在上面文章中使用过的，因此如果有在该文章中没有的则请翻看之前的文章，谢谢！ 通过递归创建决策树： ![](http://47.100.4.8/wp-content/uploads/2018/04/34343434.png)

#创建树的函数代码
def createTree(dataSet,labels):  #输入两个参数一个是数据集一个是标签集
    classList = \[example\[-1\] for example in dataSet\]  #得到数据集中每个子列表的标签 并创建一个列表存储
    #以下为递归结束条件
    if classList.count(classList\[0\]) == len(classList):  #通过统计创建标签列表的第一个标签出现的次数来和总的长度比较 如果列表中所有标签完全相同则返回该类标签
        return classList\[0\]
    if len(dataSet\[0\]) == 1: #如果子列表中所有特征值均被使用完了只剩下标签 则返回这个列表中标签出现最多的的标签名称
        return majorityCnt(classList)
    #End
    bestFeat = chooseBestFeatureToSplit(dataSet)  #如果上面的根据当前的数据集得到最好的数据集划分方式  bestFeature按照第几个特征是最好的划分方式
    bestFeatLabel = labels\[bestFeat\] #得到列数对应的标签名称
    #print(bestFeat)
    #使用字典类型存储数
    myTree = {bestFeatLabel:{}} #将选择的特征值标签听到自己创建的数字典中
    del(labels\[bestFeat\]) #将对应的标签从原有的标签列表中删除
    featValues = \[example\[bestFeat\] for example in dataSet\] #遍历得到每个列表中最佳位置特征值
    uniqueVals = set(featValues)  #组成一个列表
    for value in uniqueVals:
        subLabels = labels\[:\] #得到去掉最佳位置的标签后的所有标签
        myTree\[bestFeatLabel\]\[value\] = createTree(splitDataSet(dataSet,bestFeat,value),subLabels) #递归的到决策树
    return myTree #每次结束返回当前节点的子决策树

  使用以及结果：

import trees

myDat,labels = trees.createDataSet()
print(myDat)
print(trees.calcShannonEnt(myDat))
i=trees.chooseBestFeatureToSplit(myDat)
print(i)
myData = trees.splitDataSet(myDat,i,1)
print(myData)

print(trees.majorityCnt(myDat))

myTree = trees.createTree(myDat,labels)
print(myTree)

![](http://47.100.4.8/wp-content/uploads/2018/04/14524.png) 自己画的图：对应上面的结果（每个键值都是一个结点对应的值都是判断是数据）： ![](http://47.100.4.8/wp-content/uploads/2018/04/23231243.png)![](http://47.100.4.8/wp-content/uploads/2018/05/23231243.png) 以上就是决策树构建的全部过程，注意的是这里得到决策树是字典类型，接下来的博文会通过使用matplotlib库来绘制决策树。 End！