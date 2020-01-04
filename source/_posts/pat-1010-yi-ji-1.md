---
title: Pat_1010（乙级）
url: 1639.html
id: 1639
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:00:34
tags:
  - pat
---

1010 一元多项式求导 （25 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805313708867584

设计函数求一元多项式的导数。（注：x​n​​（n为整数）的一阶导数为nx​n−1​​。）

### 输入格式:

以指数递降方式输入多项式非零项系数和指数（绝对值均为不超过 1000 的整数）。数字间以空格分隔。

### 输出格式:

以与输入相同的格式输出导数多项式非零项的系数和指数。数字间以空格分隔，但结尾不能有多余空格。注意“零多项式”的指数和系数都是 0，但是表示为 `0 0`。

### 输入样例:

    3 4 -5 2 6 1 -2 0
    

### 输出样例:

    12 3 -10 1 6 0

代码：
```
#include<iostream>

using namespace std;

int main(){
    int temp1,temp2;
    cin>>temp1>>temp2;
    if(temp2 == 0){
        cout<<0<<" "<<0<<endl;
    }
    else{
    while(temp2 != 0){
        cout<<temp1*temp2<<" "<<temp2-1;
        cin>>temp1>>temp2;
        if(temp2!=0){
            cout<<" ";
        }
    }
    cout<<endl;
    }
    return 0;
}
```