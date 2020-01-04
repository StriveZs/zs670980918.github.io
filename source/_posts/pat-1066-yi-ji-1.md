---
title: Pat_1066（乙级）
url: 1755.html
id: 1755
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:56:44
tags:
  - pat
---

1066 图像过滤 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805266514558976)

图像过滤是把图像中不重要的像素都染成背景色，使得重要部分被凸显出来。现给定一幅黑白图像，要求你将灰度值位于某指定区间内的所有像素颜色都用一种指定的颜色替换。

### 输入格式：

输入在第一行给出一幅图像的分辨率，即两个正整数 M 和 N（0<M,N≤500），另外是待过滤的灰度值区间端点 A 和 B（0≤A<B≤255）、以及指定的替换灰度值。随后 M 行，每行给出 N个像素点的灰度值，其间以空格分隔。所有灰度值都在 \[0, 255\] 区间内。

### 输出格式：

输出按要求过滤后的图像。即输出 M 行，每行 N 个像素灰度值，每个灰度值占 3 位（例如黑色要显示为 `000`），其间以一个空格分隔。行首尾不得有多余空格。

### 输入样例：

    3 5 100 150 0
    3 189 254 101 119
    150 233 151 99 100
    88 123 149 0 255
    

### 输出样例：

    003 189 254 000 000
    000 233 151 099 000
    088 000 000 000 255

代码：
```
#include<iostream>

using namespace std;

//统计如果小于100则需要补零的个数
int countZero(int t){
    if(t - 10 < 0){
        return 2;
    }
    else{
        return 1;
    }
}

int main(){
    int N,M,A,B,T;
    cin>>N>>M>>A>>B>>T;
    int pic\[N\]\[M\];
    int temp;
    for(int i=0;i<N;i++){
        for(int j=0;j<M;j++){
            cin>>temp;
            if(temp>=A&&temp<=B){
                pic\[i\]\[j\] = T;
            }
            else{
                pic\[i\]\[j\] = temp;
            }
        }
    }
    for(int i=0;i<N;i++){
        for(int j=0;j<M;j++){
            if(j != 0){
                cout<<" ";
            }
            if(pic\[i\]\[j\] < 100){
                int m = countZero(pic\[i\]\[j\]);
                for(int q=0;q<m;q++){
                    cout<<0;
                }
            }
            cout<<pic\[i\]\[j\];
        }
        cout<<endl;
    }
    return 0;
}
```