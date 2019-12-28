---
title: 使用最小二乘法来拟合直线（C++&Python）
url: 707.html
id: 707
categories:
  - C&amp;C++
  - python数据分析
  - 文章页
  - 算法
date: 2018-04-28 23:07:29
tags:
---

  使用最小二乘法来拟合直线：   给定一个简单的直线模型y（a）=ax+b 这个问题称为直线回归。设变量y随自变量x变化，给出n组测试数据（xi，yi）用直线来拟合这些点，其中a，b是直线的斜率和截距。称为回归系数。 直线的拟合在机器学习中logistic回归时对数据进行拟合时便用到了。因此在这里给出一个详细解释。   为了确定回归系数，通常采用最小二乘法来确定，只要使式子达到最小即可。 根据极值原理，a和b满足下列方程： 根据上面式子再整合，得到如下式子： ![](http://47.100.4.8/wp-content/uploads/2018/04/66666666666666.png) 其实只需要记住上面的式子就好了。推导过程你不是数学专业的根本不需要知道。 上面的是式子就是求回归系数的主要依据。   C++实现：

#include <iostream>
#include <cmath>

using namespace std;
//直线拟合函数
float lineFit(float points\[\]\[2\],int n)  //n为点的组数 格式为：(x,y)
{
    float avgX=0,avgY=0;
    float lxx=0,lyy=0,lxy=0;
    //计算xy的平均值
    for(int i=0;i<n;i++)
    {
        avgX += points\[i\]\[0\]/n;
        avgY += points\[i\]\[1\]/n;
    }
    //计算出Lxx，Lyy，Lxy
    for(int i=0;i<n;i++)
    {
        lxx +=(points\[i\]\[0\]-avgX)*(points\[i\]\[0\]-avgX);
        lyy +=(points\[i\]\[1\]-avgY)*(points\[i\]\[1\]-avgY);
        lxy +=(points\[i\]\[0\]-avgX)*(points\[i\]\[1\]-avgY);
    }
    cout<<"函数模型为：y=ax+b"<<endl;
    cout<<"其中a="<<lxy/lxx<<"  b="<<avgY-lxy*avgX/lxx<<endl;
    float t=(lxy/sqrt(lxx*lyy));
    return t;
}

int main()
{
    float a\[10\]\[2\]={6,10,14,20,26,30,33,40,46,50,54,60,67,70,75,80,84,90,100,100};//用于测试
    float t=lineFit(a,10);
    cout<<"回归系数为："<<t<<endl;
    return 0;
}

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/3333333333333.png) python使用numpy实现：  numpy要好好学了。。搞了半天才弄好数组计算

import numpy as np
import re
import math

#处理文本文件   信息格式为（x，y）
def loadData():   
    dataSet = \[\]
    dataSave = open('F:/StraightFitting.txt')
    for line in dataSave.readlines():
        lineArr = re.compile(r'\[0-9\]*\[0-9\]+')
        save = lineArr.findall(line)
        dataSet.append(save)
    return dataSet

def LineFit(dataSet):
    dataMatrix = np.array(dataSet,dtype=np.int32)
    m = np.shape(dataMatrix)\[0\]
    n = np.ndim(dataMatrix)
    avgX = sum((dataMatrix/n)\[0:m,0\])
    avgY = sum((dataMatrix/n)\[0:m,1\])
    lxx = sum((dataMatrix\[0:m,0\]-avgX)*(dataMatrix\[0:m,0\]-avgX))
    lyy = sum((dataMatrix\[0:m,1\]-avgY)*(dataMatrix\[0:m,1\]-avgY))
    lxy = sum((dataMatrix\[0:m,0\]-avgX)*(dataMatrix\[0:m,1\]-avgY))
    a = lxy / lxx
    b = avgY - lxy * avgX / lxx
    t = lxy / math.sqrt(lxx * lyy)
    return a,b,t
    
dataSet = loadData()
a,b,t=LineFit(dataSet)
print(a,b,t)

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/222222222222.png)