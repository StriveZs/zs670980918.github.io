---
title: 机器学习之SVM
url: 1398.html
id: 1398
categories:
  - 向量机支持SVM
  - 文章页
  - 机器学习
date: 2018-07-03 15:53:59
tags:
  - Machine Learning
  - SVM
  - Algorithm
---

**支持****向量机（SVM）**

序列最小化优化算法（SMO）

  基于最大间隔分隔数据 优点：泛化错误率低，计算开销不大，结果易破解 缺点：对参数调节和核函数的选择敏感，原始分类不加修改仅适用于处理二类问题 适用数据类型：数值型和标称型数据   考虑下图如何用一条直线将两组数据点分开。 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180703154529.png) 在这种情况下成为线性可分数据，上述数据集分隔开来的直线成为分隔平面（之所以为平面是统称）因为在二维空间上可以用一条直线将其分隔开来的，但是在三维空间中只能用平面来进行分隔。 同样可以类推出如果是500维的平面可以是用499维度的平面分隔，这类平面成为超平面。   我们在构建超平面的同时也希望选择出来最好的那一个超平面，比如下图中三图（BCD）哪个最好？ ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180703154619.png) 可以看出来上述做法有点类似直线拟合，这里其实和logistic回归中构建出来分隔线（也类似直线拟合）差不多。 我们希望找到离分隔超平面最近的点，确保他们离分隔面的距离尽可能远。这里点到分隔面的距离称为间隔。   支持向量就是离分隔超平面最近的那些点。   **寻找最大间隔** 如下图 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180703154733.png) 分隔超平面的形式可以写成（w的t次方\*x+b），要计算点A到分隔超平面的距离，就必须给出A到分隔面的法线或垂线的长度，该值为（|w的t次方\*a+b|/|w|） 这里的常数b类似于logistic回归中的截距W0. **分类器求解的优化问题** 理解：输入的数据分类器会输出一个类别标签，这里相当于一个类似于sigmoid的函数作用下，接下来使用的是类似海维塞德阶跃函数（即单位跃阶函数）的函数对分隔超平面函数作用得到的f（w的t次方*x+b），其中当u<0时f（u）输出-1，反之则输出1，这里与logistic回归中的函数有所不同（它用的分类标签为0和1）。 当计算数据点到分隔面的距离并确定分隔面的放置位置时，间隔用过label*（w的t次方*x+b）来计算。 通过一系列操作可以得到如下形式的优化目标函数： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180703154833.png) 其中约束条件为： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180703154903.png) 这里的C常用来控制最大化间隔和保证大部分点的函数间隔小于1.0这两个目标的权重。 通常在代码实现时C常为一个参数，因此我们可以通过改变C的参数值来得到不同的结果，一旦求出所有的alpha，那么分隔超平面就可以通过这些alpha表达。而SVM的主要工作就是求解这些alpha。 **SVM应用的一般框架** SVM的一般流程：

*   收集数据：可以使用任何方法
*   准备数据：需要数值型数据
*   分析数据：有助于可视化分隔超平面（matplotlib）
*   训练算法：SVM的大部分时间都是源自训练，该过程主要实现两个参数（w，b）的调优。
*   测试算法：十分简单的计算过程就可以实现
*   使用算法：几乎所有分类分为都可以使用SVM，SVM是二分类器，对于多类问题使用SVM的话需要对代码进行修改

**SMO高效优化算法** SMO算法是JohnPlatt发现的，用于训练SVM，SMO表示序列最小优化，Platt的SMO算法是将大优化问题分解为小的优化问题（有点类似分治的思想）。SMO的目标是求出一系列的alpha和b，一旦求出来这些alpha就方便计算出权重向量w并得到分隔超平面。 首先给出一个简单的版本来方便理解（该算法适合小规模的数据集但是执行速度比较慢）： 读取数据以及随机一个整数并且对该整数的大小进行调整函数 代码：
```
#SMO算法中的辅助函数
def loadDataSet(fileName):  #读取数据和标签
    dataMat = \[\]
    labelMat = \[\]
    fr = open(fileName)
    for line in fr.readlines():
        lineArr = line.strip().split('\\t')
        dataMat.append(\[float(lineArr\[0\]),float(lineArr\[1\])\])
        labelMat.append(float(lineArr\[2\]))
    return dataMat,labelMat

def selectJrand(i,m):  #在某一范围内得到一个随机整数
    j=i
    while(j==i):
        j = int(random.uniform(0,m))
    return j

def clipAlpha(aj,H,L):  #辅助函数用于对如果随机数据太大来进行调整
    if aj > H:
        aj = H
    if L > aj:
        aj = L
return aj
```
对于selectJrand函数中i是第一个aplha的下标，m是所有alpha的数目，只要函数的值不等于i的值则一直会随机。 SMO函数的伪代码： 创建一个alpha向量并将其初始化为0向量 当迭代次数小于最大迭代次数时：（外循环）    对数据中的每一个数据向量：（内循环）        如果该数据向量可以被优化：           随机选择另外一个数据向量           同时优化这两个向量           如果这两个向量都不能被优化，退出内循环    如果所有向量都没有被优化，增加迭代数目，继续下一次循环 下面给出代码：
```
def SMOSimple(dataMatIn,classLabels,C,toler,maxIter): #五个参数：数据集、类别标签、常数C、容错率、最大循环次数
    dataMatrix = np.mat(dataMatIn)
    labelMat = np.mat(classLabels).transpose() #对标签进行转置，将其转置为列向量
    b = 0
    m,n = np.shape(dataMatrix)  #得到矩阵的行和列数
    alphas = np.mat(np.zeros((m,1))) #创建一个alpha矩阵，并且以zeros初始化
    iter = 0  #用来存储在alphas没有任何变化的情况下遍历数据集的次数
    while(iter < maxIter):
        alphaPairsChanged = 0  #用于记录alphas是否被优化
        for i in range(m):
            fXi = float(np.multiply(alphas,labelMat).T * (dataMatrix * dataMatrix\[i,:\].T)) + b  #fXi用于表示预测的类别
            Ei = fXi - float(labelMat\[i\])  #计算预测值和实际值的误差
            if ((labelMat\[i\] * Ei < -toler) and (alphas\[i\] < C)) or ((labelMat\[i\] * Ei > toler) and (alphas\[i\] > 0)): #如果不在最大允许误差的范围内则对alphas进行优化
                j = selectJrand(i,m) #使用辅助函数随机选择出第二个alphas值的下标
                fXj = float(np.multiply(alphas,labelMat).T * (dataMatrix * dataMatrix\[j,:\].T)) + b #同样采用之前的误差计算方法来对第二个alphas进行判断
                Ej = fXj - float(labelMat\[j\])
                #复制新老alphas对进行比较
                alphaIold = alphas\[i\].copy() 
                alphaJold = alphas\[j\].copy()
                if (labelMat\[i\] != labelMat\[j\]):  #计算LH的值
                    L = max(0,alphas\[j\] - alphas\[i\])
                    H = min(C,C + alphas\[j\] - alphas\[i\])
                else:
                    L = max(0,alphas\[j\] + alphas\[i\] - C)
                    H = min(C,alphas\[j\] + alphas\[i\])
                if L == H: #如果L和H的值相等则结束本次循环
                    print("L==H")
                    continue
                #eta是alphas\[j\]的最优秀改量
                eta = 2.0 * dataMatrix\[i,:\] * dataMatrix\[j,:\].T - dataMatrix\[i,:\] * dataMatrix\[i,:\].T - dataMatrix\[j,:\] * dataMatrix\[j,:\].T
                if eta >= 0:
                    print("eta>=0")
                    continue
                #对第二个alphas值进行更新
                alphas\[j\] -= labelMat\[j\] + (Ei - Ej) / eta
                alphas\[j\] = clipAlpha(alphas\[j\],H,L)#并且进行调整
                if (abs(alphas\[j\] - alphaJold) < 0.00001):  #如果最新的得到的第二个alphas值和旧的值相差不够大则结束本次循环
                    print("j 移动的不够充分")
                    continue
                #更新第一个alphas值
                alphas\[i\] += labelMat\[j\] * labelMat\[i\] * (alphaJold - alphas\[j\])
                #分别根据第一个alphas值和第二个alphas值来计算出b1和b2
                b1 = b - Ei - labelMat\[i\] * (alphas\[i\] - alphaIold) * dataMatrix\[i,:\].T - labelMat\[j\] * (alphas\[j\] - alphaJold) * dataMatrix\[i,:\] * dataMatrix\[j,:\].T
                b2 = b - Ej - labelMat\[i\] * (alphas\[i\] - alphaIold) * dataMatrix\[i,:\].T - labelMat\[j\] * (alphas\[j\] - alphaJold) * dataMatrix\[j,:\] * dataMatrix\[j,:\].T
                #根据约束条件的公式来决定b的值
                if(0 < alphas\[i\] and (C > alphas\[i\])):
                    b = b1
                elif(0 < alphas\[j\]) and (C > alphas\[j\]):
                    b = b2
                else:
                    b = (b1 + b2) / 2.0
                alphaPairsChanged += 1  #记录alphas被优化更改值的次数
                print("iter: %d  i:%d,pairs changed %d"%(iter,i,alphaPairsChanged))
        if(alphaPairsChanged == 0):  #用于判断alphas是否被优化如果没有被优化则iter+1
            iter += 1
        else :
            iter = 0
        print("iteration number: %d" % iter)
    return b,alphas
```
主要的原理还是几个预测公式，这个是前人推出来的，我有点看不懂但是直接用还是可以的。 这个函数写的累死我了光看书写就写了好久。 函数的五个参数为：数据集、类别标签、常数C、容错率、最大循环次数 np.mat（）函数作用是：将数组转换为二维的numpy矩阵，它和ndarray数组又有一些区别。 使用np.mat(classLabels).transpose() 是将行标签转置为了列向量，方便和矩阵每行进行对应。 使用zeros创建一个初始化长度为m的numpy数组并将其转换为矩阵，用来表示alphas 注：该alphas就是之前条件公式里面的阿尔法 创建iter 用来存储在alphas没有改变的情况下遍历数据集的次数，当该值达到最大循环次数时则结束。

1.  Multiply（）用来将两个矩阵/向量相乘 然后.T 是得到转置

fXi = float(np.multiply(alphas,labelMat).T * (dataMatrix * dataMatrix\[i,:\].T)) + b  fXi用于表示预测值， Ei表示预测值和实际值的误差，如果误差很大则需要对alphas进行优化 eta是alphas\[j\]的最优秀改量 b的值是要结合eta的值以及得到最新的alphas值来计算。   由于是简单的SMO算法所以时间效率比较低下，空间资源利用不足，但是便于理解。 以上先给出一个简单的SMO方便用于理解，至于复杂的SMO算法在以后给出。