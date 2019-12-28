---
title: Python实现快速排序并且对sort进行介绍
url: 1592.html
id: 1592
categories:
  - Python功能
  - Python知识
  - 文章页
date: 2019-01-19 17:14:01
tags:
---

![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190119170830.png)        通过键盘接收若干个整数，存放在列表中。使用Python实现快速排序并将结果输出，并且进行和自带的sort函数相比进行性能分析。

import copy
import time
import random

#快排
def once_sort(num,low,high):
    d = num\[low\]
    while low<high:
        while low<high and num\[high\] >= d:
            high = high - 1
        while low < high and num\[high\] < d:
            num\[low\] = num\[high\]
            low = low + 1
            num\[high\] = num\[low\]
    num\[low\] = d
    return low

def quick_sort(num,low,high):
    if low<high:
        d = once_sort(num,low,high)
        quick_sort(num,low,d)
        quick_sort(num,d+1,high)
    return num
#性能分析
def analy():
    randnum = \[x for x in range(1000000)\] #生成一万个整数
    random.shuffle(randnum)
    randnum1 = copy.deepcopy(randnum)
    print('使用快速排序进行一百万数排序所花费的时间：',end='')
    start1 = time.clock()
    quick_sort(randnum,0,len(list(randnum))-1)
    finish1 = time.clock()
    print(finish1-start1)
    print('使用列表自带的sort排序函数进行一百万数排序所花费的时间：', end='')
    start1 = time.clock()
    randnum1.sort()
    finish1 = time.clock()
    print(finish1 - start1)

if \_\_name\_\_ == '\_\_main\_\_':
    strnum = input('输入一串数字，数字之间以逗号分隔开：')
    num = strnum.split(',')
    num1 = \[int(x) for x in num\]
    num2 = copy.deepcopy(num1)
    print('列表形式:', end='')
    print(num1)
    low = 0
    high = len(num1)-1
    num1 = quick_sort(num1,low,high)
    print('排序之后的结果为：',end='')
    print(num1)
    print('使用列表自带的sort函数排序的结果为：',end='')
    num2.sort()
    print(num2)
    #算法性能的分析
    analy()

结果： ![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190119171031.png) 下面是通过查阅资料得到的对自带的sort函数进行的介绍： 它使用的是Timesort原理，timesort是结合了合并排序和插入排序而得出的排序算法。该算法为了减少对升序部分的回溯和对降序部分的性能倒退，将输入的数值按照升序和降序的特点进行了分区。因此排序的单位不是一个个数字而是一个个块-分区。其中每个分区叫一个run，针对这些run序列，每次拿一个run出来按规则进行合并。每次合并会将两个run合并为一个run，合并的结果保存到栈中，知道所有的run都被使用，这时将栈中所有的run合并到只剩一个run，这个run便是排序好的结果。 Timesort和快排之间的性能比较： ![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190119171150.png) 这里对timesort算法的了解参考了如下文章： https://blog.csdn.net/yangzhongblog/article/details/8184707