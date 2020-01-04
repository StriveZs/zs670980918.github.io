---
title: Pat_1050（乙级）
url: 1723.html
id: 1723
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:30:36
tags:
  - pat
---

1050 螺旋矩阵 （25 分）[原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805275146436608)

本题要求将给定的 N 个正整数按非递增的顺序，填入“螺旋矩阵”。所谓“螺旋矩阵”，是指从左上角第 1 个格子开始，按顺时针螺旋方向填充。要求矩阵的规模为 m 行 n 列，满足条件：m×n 等于 N；m≥n；且 m−n 取所有可能值中的最小值。

### 输入格式：

输入在第 1 行中给出一个正整数 N，第 2 行给出 N 个待填充的正整数。所有数字不超过 10​4​​，相邻数字以空格分隔。

### 输出格式：

输出螺旋矩阵。每行 n 个数字，共 m 行。相邻数字以 1 个空格分隔，行末不得有多余空格。

### 输入样例：

    12
    37 76 20 98 76 42 53 95 60 81 58 93
    

### 输出样例：

    98 95 93
    42 37 81
    53 20 76
    58 60 76

代码：
```
#include<iostream>
#include<math.h>
#include<algorithm>

using namespace std;

bool cmp(int a,int b){
    return a > b;
}
int main(){
    int m,n,num,t;
    cin>>num;
    int list1\[num\];
    for(int i=0;i<num;i++){
        cin>>list1\[i\];
    }
    sort(list1,list1+num,cmp);
    /*for(int i=0;i<num;i++){
        cout<<list1\[i\]<<" ";
    }
    cout<<endl;*/
    n = floor(sqrt(num));
    m = int(num / n);
    while(n*m != num){
        n--;
        m = int(num / n);
    }
    if(n > m){
        t = n;
        n = m;
        m = t;
    }
    int result\[m\]\[n\];
    for(int i=0;i<m;i++){
        for(int j=0;j<n;j++){
            result\[i\]\[j\] = 0;
        }
    }
    int heng,zong,index=0,dire=0; //dire为方向 0向右移动  1向下移动  2向左移动 3向上移动
    heng = 0;
    zong = 0;
    while(index < num){
        result\[heng\]\[zong\] = list1\[index\];
        //cout<<heng<<" "<<zong<<endl;
        if(dire == 0){ //向右
            if(zong < n-1){
                if(result\[heng\]\[zong+1\] == 0){
                    zong++;
                }
                else{
                    dire = 1;
                    heng++;
                }
            }
            else{
                dire = 1;
                heng++;
            }
        }
        else if(dire == 1){
            if(heng < m-1){ //向下
                if(result\[heng+1\]\[zong\] == 0){
                    heng++;
                }
                else{
                    dire = 2;
                    zong--;
                }
            }
            else{
                dire = 2;
                zong--;
            }
        }
        else if(dire == 2){
            if(zong > 0){ //向左
                if(result\[heng\]\[zong-1\] == 0){
                    zong--;
                }
                else{
                    dire = 3;
                    heng--;
                }
            }
            else{
                dire = 3;
                heng--;
            }
        }
        else if(dire == 3){
            if(heng > 0){ //向上
                if(result\[heng-1\]\[zong\] == 0){
                    heng--;
                }
                else{
                    dire = 0;
                    zong++;
                }
            }
            else{
                dire = 0;
                zong++;
            }
        }
        index++;
    }
    for(int i=0;i<m;i++){
        for(int j=0;j<n;j++){
            if(j == 0){
                cout<<result\[i\]\[j\];
            }
            else{
                cout<<" "<<result\[i\]\[j\];
            }
        }
        cout<<endl;
    }
    return 0;
}
```