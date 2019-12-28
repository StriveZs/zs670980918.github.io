---
title: 机器学习之朴素贝叶斯
url: 670.html
id: 670
categories:
  - 文章页
  - 朴素贝叶斯
date: 2018-04-23 18:13:43
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) 称为朴素的原因：是因为整个形式化过程只做最原始、最简单的假设。 任务：利用python进行文本处理将文档切分成词向量，然后利用词向量对文档进行分类。 朴素贝叶斯使用数据类型：标称型数据 优点是：在数据较少的情况下仍然能使用，可以处理多类别问题。 缺点：对于数据输入方式有一定要求。   快速了解贝叶斯决策理论： 用p1(x,y)表示数据点(x,y)属于类别1的概率 用p2(x,y)表示数据点(x,y)属于类别2的概率 那么对于一个 新的数据点(x,y)我们使用如下规则判断它属于哪个类别： p1(x,y)>p2(x,y) —>属于类别1 p1(x,y)<p2(x,y) —>属于类别2 因此就是我们只会选择高概率对应的类别即高概率决策。这就是贝叶斯思想的核心。（由此可见之后要使用到概率论的知识。） 贝叶斯决策时最佳的数据点分类策略。   主要用到了条件概率： p（A|B）=P（AB）/P（B） 贝叶斯准则：计算条件概率的方法：已知p(A|B)求P（B|A），可已使用如下公式计算 P（B|A）=（P(A|B)*P(B)）/P(A)   使用条件概率来分类： 上面提到的核心思想并不是贝叶斯决策的全部内容，p1（）和p2（）也不是真实的只是一个表示：实际为p（c1|x，y）和p（c2|x，y）这些符号所代表的的具体意义是给定某个x、y表示的数据点，那么该点来自c1或者c2类别的概率多少 应用贝叶斯准则得到： ![](http://47.100.4.8/wp-content/uploads/2018/04/123341233123.png) 分类过程就是按照谁的概率更大一些就属于它所在分类。   使用朴素贝叶斯进行文档分类：   过程：

1.  收集数据：可以使用任何方法，这里使用的是RSS源
2.  准备数据：需要数值型或者布尔型数据。
3.  分析数据：有大量特征值时，绘制特征作用不大，此时使用直方图比较好
4.  训练算法：计算不同的独立特征的条件概率。
5.  测试算法：计算错误率

使用算法：一个常见的的朴素贝叶斯应用的文档的分类   特征值之间要相互独立，即一个特征出现的可能性与其他特征值无关。 朴素贝叶斯分类器中的另一种假设是：每个特征值同等重要。     使用python进行文本分类： 首先要进行文本的拆分：特征是来自文本的一个词条，一个词条是字符的任意组合。 接下来以在线社区留言板为例： 目的是屏蔽侮辱性的言论，因此构建一个快速过滤侮辱性言论的过滤器。 将文本内容分为侮辱性和非侮辱性使用1和0分别表示   接下来就是将文本转换为数字向量   准备数据：从文本中构建词向量（也就是将句子转换为向量） 词表到向量的转换函数：

import numpy as np
#词表到向量的转化函数
#创建一些实验样本 用于训练
def loadDataSet():
    postingList = \[\['my','dog','has','flea','problems','help','please'\],
                   \['maybe','not','take','him','to','dog','park','stupid'\],
                   \['my','dalmation','is','so','cute','I','love','him'\],
                   \['stop','posting','stupid','worhless','garbage'\],
                   \['mr','licks','ate','my','steak','how','to','stop','him'\],
                   \['quit','buying','worhless','dog','food','stupid'\]\]
    #创建一个类别标签集合
    classVec = \[0,1,0,1,0,1\] #每一个标签对应一个子列表 分别表示了是侮辱性语言（1）还是非侮辱性语言（0） 
    return postingList,classVec

#处理集合 创建一个包含在所有文档中出现的不重复词的列表
def createVocableList(dataSet):
    vocabSet = set(\[\]) #创建一个无序无重复空集
    for document in dataSet:
        vocabSet = vocabSet | set(document)  #创建两个集合的并集 目的是去掉dataSet中每个集合重复的数据
    return list(vocabSet)
#创建一个将给的文档转换为向量文档的函数
#该函数的输入参数为词汇表以及某个文档
def setOfWords2Vec(vocabList,inputSet):
    returnVec = \[0\]*len(vocabList)  #创建一个词汇表等长的向量表
    for word in inputSet:#循环遍历输入的文档
        if word in vocabList: #如果输入的文档内容在给出的 词汇表中
            returnVec\[vocabList.index(word)\] = 1 #找到word对应的索引位置并且将返回数字向量对应的位置设置为1
        else:
            print("这个单词是：%s 不在我的词表中!" %word)
    return returnVec  #输出的是向量文档

使用：

import Bayesian

listOposts,listClasses = Bayesian.loadDataSet()
myVocabList = Bayesian.createVocableList(listOposts)
print(myVocabList)
print(listClasses)
print(Bayesian.setOfWords2Vec(myVocabList,listOposts\[0\]))

结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/sad中心擦伤的.png)![](http://47.100.4.8/wp-content/uploads/2018/04/1968541563156.png) End！