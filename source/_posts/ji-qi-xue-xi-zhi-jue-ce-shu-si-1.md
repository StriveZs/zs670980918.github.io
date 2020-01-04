---
title: 机器学习之决策树（四）
url: 638.html
id: 638
categories:
  - 决策树
  - 机器学习
date: 2018-04-19 22:56:20
tags:
  - Decision Tree
  - Algorithm
  - Machine Learning
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) 使用matplotlib绘制决策树： 构造注解树： 首先要得到树的子节点数目和树的深度 都是通过递归得到的 首先是递归得到树的叶子结点数目：
```
#深度递归遍历获取树的叶节点数目
def getNumLeafs(myTree):
    numLeafs = 0
    firstStr = list(myTree.keys())\[0\]  #得到字典的第一个键值
    secondDict = myTree\[firstStr\] ##得到键值对应的值（子字典）
    for key in secondDict.keys():
        #判断得到的数据是否为字典
        if type(secondDict\[key\]).\_\_name\_\_ == 'dict':  #如果仍为字典类型 则进行再次的深度递归遍历 访问他的子节点（子字典）
            numLeafs += getNumLeafs(secondDict\[key\])
        else:
            numLeafs +=1 #如果访问的类型不是字典 则证明已经访问到了一个具体的值 则进行节点数+1
    return numLeafs

  如果想要详细的了解过程，可以用过Debug来查看值   然后是递归得到树的层数：

#获得树的层数
def getTreeDepth(myTree):
    maxDepth = 0  #初始化最大深度
    firstStr = list(myTree.keys())\[0\]  #得到字典的第一个键值
    secondDict = myTree\[firstStr\] #得到键值对应的值（子字典）
    for key in secondDict.keys():
        #判断得到的数据是否为字典
        if type(secondDict\[key\]).\_\_name\_\_ == 'dict':  #如果仍为字典类型 则进行再次的深度递归遍历 访问他的子节点（子字典）
            thisDepth = 1 + getTreeDepth(secondDict\[key\])
        else:
            thisDepth = 1 #如果遇到叶子节点则返回
        if thisDepth > maxDepth:
            maxDepth = thisDepth
    return maxDepth

  使用以之前创建的树为例子： ![](http://47.100.4.8/wp-content/uploads/2018/04/543234.png)![](http://47.100.4.8/wp-content/uploads/2018/04/526325.png) 结果：![](http://47.100.4.8/wp-content/uploads/2018/04/213213.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/82236633.png) 绘制决策树： 要使用到上面的函数getNumLeafs（得到树的叶子结点），getTreeDepth（得到树的层数） 具体形式：

trees.getNumLeafs(myTree)
trees.getTreeDepth(myTree)

绘制带注解的箭头：

#绘制带箭头的注解
def plotNode(nodeTxt,centerPt,parentPt,nodeType):
    createPlot.ax1.annotate(nodeTxt,xy=parentPt,xycoords='axes fraction',xytext=centerPt,\
                            textcoords='axes fraction',va="center",ha="center",\
                            bbox=nodeType,arrowprops=arrow_args)

  在父子结点间填充信息：

#在父子结点间填充信息
def plotMidText(cntrPt,parentPt,txtString):
    xMid = (parentPt\[0\] - cntrPt\[0\]) / 2.0 + cntrPt\[0\]
    yMid = (parentPt\[1\] - cntrPt\[1\]) / 2.0 + cntrPt\[1\]
    createPlot.ax1.text(xMid,yMid,txtString)

  得到绘制树的相关数据：

#plotTree函数
def plotTree(myTree,parentPt,nodeTxt):
    numLeafs = getNumLeafs(myTree)
    depth = getTreeDepth(myTree)
    firstStr = myTree.keys()\[0\]
    cntrPt = (plotTree.xOff + (1.0 + float(numLeafs)) / 2.0 / plotTree.totalW,plotTree.yOff)
    plotMidText(cntrPt,parentPt,nodeTxt)
    plotNode(firstStr,cntrPt,parentPt,decisionNode)
    secondDict = myTree\[firstStr\]
    plotTree.xOff = plotTree.yOff - 1.0 / plotTree.totalD
    for key in secondDict.keys():
        if type(secondDict\[key\]).\_\_name\_\_ == 'dict':
            plotTree(secondDict\[key\],cntrPt,str(key))
        else:
            plotTree.xOff = plotTree.xOff + 1.0 / plotTree.toatlW
            plotNode(secondDict\[key\],(plotTree.xOff,plotTree.yOff),cntrPt,leafNode)
            plotMidText((plotTree.xOff,plotTree.yOff),cntrPt,leafNode)
    plotTree.yOff = plotTree.yOff + 1.0 / plotTree.totalD

  绘制树：

def createPlot(inTree):
    fig = plt.figure(1,facecolor='white')
    fig.clf()
    axprops = dict(xticks=\[\],ticks=\[\])
    createPlot.ax1 = plt.subplot(111,frameon=False,**axprops)
    plotTree.totalW = float(getNumLeafs(inTree))
    plotTree.totalD = float(getTreeDepth(inTree))
    plotTree.xOff = -0.5 / plotTree.totalW;plotTree.yOff = 1.0;
    plotTree(inTree,(0.5,1.0),'')
    plt.show()

  两个测试字典（树）：

#示例的两个字典
def retrieveTree(i):
    listOfTree = \[{'no surfacing':{0:'no',1:{'flippers':{0:'no',1:'yes'}}}},
                  {'no surfacing':{0:'no',1:{'flippers':{0:{'head':{0:'no',1:'yes'}},1:'no'}}}}
                  \]
    return listOfTree\[i\]
```
  效果图： ![](http://47.100.4.8/wp-content/uploads/2018/04/6435.png)![](http://47.100.4.8/wp-content/uploads/2018/04/8523652.png)   End！