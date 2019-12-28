---
title: Pat_1045（乙级）
url: 1713.html
id: 1713
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:23:06
tags:
---

1045 快速排序 （25 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805278589960192)

著名的快速排序算法里有一个经典的划分过程：我们通常采用某种方法取一个元素作为主元，通过交换，把比主元小的元素放到它的左边，比主元大的元素放到它的右边。 给定划分后的 N 个互不相同的正整数的排列，请问有多少个元素可能是划分前选取的主元？ 例如给定 $N = 5$, 排列是1、3、2、4、5。则：

*   1 的左边没有元素，右边的元素都比它大，所以它可能是主元；
*   尽管 3 的左边元素都比它小，但其右边的 2 比它小，所以它不能是主元；
*   尽管 2 的右边元素都比它大，但其左边的 3 比它大，所以它不能是主元；
*   类似原因，4 和 5 都可能是主元。

因此，有 3 个元素可能是主元。

### 输入格式：

输入在第 1 行中给出一个正整数 N（≤10​5​​）； 第 2 行是空格分隔的 N 个不同的正整数，每个数不超过 10​9​​。

### 输出格式：

在第 1 行中输出有可能是主元的元素个数；在第 2 行中按递增顺序输出这些元素，其间以 1 个空格分隔，行首尾不得有多余空格。

### 输入样例：

    5
    1 3 2 4 5
    

### 输出样例：

    3
    1 4 5

代码：

#include<iostream>
#include<algorithm>

using namespace std;
//思路：将数组排序，排序后的结果和原来的数组比较如果相同位置的数字相同也是不会小于之前（包含自己）的最大值 则为主元
bool cmp(int a,int b){
    return a < b;
}

int main(){
    long int len,sum=0;
    cin>>len;
    long int num\[len\],goal\[len\],result\[len\];
    for(long int i=0;i<len;i++){
        cin>>num\[i\];
        goal\[i\] = num\[i\];
    }
    sort(num,num+len,cmp);
    long int maxx = 0;
    for(long int i=0;i<len;i++){
        if(goal\[i\] > maxx){
            maxx = goal\[i\];
        }
        if(goal\[i\] == num\[i\] && num\[i\] == maxx){
            result\[sum\] = num\[i\];
            sum++;
        }
    }
    cout<<sum<<endl;
    for(long int i=0;i<sum;i++){
        if(i == sum-1){
            cout<<result\[i\];
        }
        else{
            cout<<result\[i\]<<" ";
        }
    }
    cout<<endl;
    return 0;
}