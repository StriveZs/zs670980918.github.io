---
title: logistic回归之梯度上升算法
url: 716.html
id: 716
categories:
  - logistic回归
  - 文章页
  - 机器学习
date: 2018-04-30 23:43:00
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) **梯度**：在微积分里面，对多元函数的参数求∂偏导数，把求得的各个参数的偏导数以向量的形式写出来，就是梯度。 它几何上的意义是：函数变化增加最快的地方。也就是在（x，y）点处沿梯度方向就是增长最快的地方 回归系数的确定： 基于最优化方法的最佳回归系数确定的算法： **梯度上升法算法** 梯度上升的思想是：要找到某函数的最大值，最好的方法是沿着该函数的梯度方向探寻。 如果记梯度为▽则函数f（x，y）的梯度由 ![](http://47.100.4.8/wp-content/uploads/2018/04/1.png)表达。   这个式子不是要去懂是如何去实现的，要了解这些符号的意思： ![](http://47.100.4.8/wp-content/uploads/2018/04/2.png)表示的是要在沿x的方向上移动![](http://47.100.4.8/wp-content/uploads/2018/04/2.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/3.png)表示的是在沿y的方向上移动![](http://47.100.4.8/wp-content/uploads/2018/04/3.png) 其中f（x，y）必须要在计算的点上有定义且可微。 一个具体的例子： 梯度上升算法是每到达一个点就重新估计运行的方向。 ![](http://47.100.4.8/wp-content/uploads/2018/05/54134894.png) 在从P0点开始，计算完该点的梯度，函数会根据该点的梯度继续移动，在到达P1点时再次重新计算在P1点梯度，然后沿着该梯度向P2点移动，直到运行到满足条件的位置。 这样就能确保每次都是沿着最佳的方向移动。   梯度算子总是指向函数值增长最快的方向。移动量的大小称为步长，记为α。 迭代公式为：![](http://47.100.4.8/wp-content/uploads/2018/04/4.png) 该公式一直被迭代使用，直到满足特定的条件为止。 训练算法：使用梯度上升找到最佳参数 梯度上升的伪代码： 每个回归系数初始化为1 重复R次： 计算整个数据集的梯度 使用alpha*gradient更新回归系数的向量 返回回归系数   梯度上升算法的局限性：他只能处理100左右的数据集，但是要是涉及成千上万次的特征值时，使用该算法的时间复杂度就会很高。

import numpy as np



#数据读取和处理函数
def loadDataSet():
    dataMat = \[\]
    labelMat = \[\]
    fr = open('testSet.txt')
    for line in fr.readlines():
        lineArr = line.strip().split()
        dataMat.append(\[2.0,float(lineArr\[0\]),float(lineArr\[1\])\])   #读取前两个字符作为X1和X2
        labelMat.append(int(lineArr\[2\]))  #读取后面的标签
    return dataMat,labelMat

#sigmoid 函数
def sigmoid(inX):
    return 1.0/(1 + np.exp(-inX)) #公式

#梯度上升优化算法
def gradAscent(dataMatIn,classLabels):
    #dataMatIn是一个二维numpy数组每一列分别代表每个不同的特征，每行则代表每个训练样本
    dataMatrix = np.mat(dataMatIn)
    labelMat = np.mat(classLabels).transpose()
    #上面是将数据转换为numpy矩阵
    m,n = np.shape(dataMatrix)
    alpha = 0.001  #是步长
    maxCycle = 500  #迭代次数
    weight = np.ones((n,1)) #初始化最佳参数 numpy矩阵的n是dataMatrix中的列数也就是每个数据特征值的个数
    #矩阵相乘
    for k in range(maxCycle): #进行maxCycle词迭代
        example = dataMatrix * weight  #实现的是三个特征值乘以weight然后相加
        h = sigmoid(dataMatrix * weight)  #调用sigmoid函数得到每个数据通过使用sigmoid计算得到的值 位于0-1之间
        error = (labelMat - h)  #通过计算原值和分类值的差值
        example1 = dataMatrix.transpose()  #矩阵转置
        weight = weight + alpha * dataMatrix.transpose() * error  #按照差值的重新调整回归系数
return weight  #返回新的回归系数

 

import logRegres

dataArr,labelMat = logRegres.loadDataSet()
print(dataArr,labelMat)
print(logRegres.gradAscent(dataArr,labelMat))

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/5.png) 详细的代码运行过程，可以通过debug自行去了解，这里我推荐使用spyder 它的debug调试过程能够清楚的看到每个数据。