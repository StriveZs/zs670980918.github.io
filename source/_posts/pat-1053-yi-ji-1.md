---
title: Pat_1053（乙级）
url: 1729.html
id: 1729
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:34:29
tags:
  - pat
---

1053 住房空置率 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805273284165632)

在不打扰居民的前提下，统计住房空置率的一种方法是根据每户用电量的连续变化规律进行判断。判断方法如下：

*   在观察期内，若存在超过一半的日子用电量低于某给定的阈值 e，则该住房为“可能空置”；
*   若观察期超过某给定阈值 D 天，且满足上一个条件，则该住房为“空置”。

现给定某居民区的住户用电量数据，请你统计“可能空置”的比率和“空置”比率，即以上两种状态的住房占居民区住房总套数的百分比。

### 输入格式：

输入第一行给出正整数 N（≤1000），为居民区住房总套数；正实数 e，即低电量阈值；正整数 D，即观察期阈值。随后 N 行，每行按以下格式给出一套住房的用电量数据： K E​1​​ E​2​​ ... E​K​​ 其中 K 为观察的天数，E​i​​ 为第 i 天的用电量。

### 输出格式：

在一行中输出“可能空置”的比率和“空置”比率的百分比值，其间以一个空格分隔，保留小数点后 1 位。

### 输入样例：

    5 0.5 10
    6 0.3 0.4 0.5 0.2 0.8 0.6
    10 0.0 0.1 0.2 0.3 0.0 0.8 0.6 0.7 0.0 0.5
    5 0.4 0.3 0.5 0.1 0.7
    11 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1
    11 2 2 2 1 1 0.1 1 0.1 0.1 0.1 0.1
    

### 输出样例：

    40.0% 20.0%
    

（样例解释：第2、3户为“可能空置”，第4户为“空置”，其他户不是空置。）

代码：
```
#include<iostream>
#include<cstdio>

using namespace std;

int main(){
    int num;
    float e,D,maybe\_num=0,must\_num=0;
    cin>>num>>e>>D;
    for(int i=0;i<num;i++){
        bool maybe\_flag = false,must\_flag = false;
        int temp;
        float t=0,sum=0;
        cin>>temp;
        for(int j=0;j<temp;j++){
            cin>>t;
            if(t < e){
                sum++;
            }
        }
        if(sum > temp/2){
            maybe_flag = true;
        }
        if(maybe_flag && temp > D){
            must_flag = true;
        }
        if(must_flag){
            must_num++;
        }
        else if(maybe_flag){
            maybe_num++;
        }
    }
    printf("%0.1f%% %0.1f%%\\n",(maybe\_num/num)\*100,(must\_num/num)\*100);
    return 0;
}
```