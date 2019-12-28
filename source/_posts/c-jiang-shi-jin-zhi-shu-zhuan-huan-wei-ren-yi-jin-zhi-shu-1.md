---
title: C++将十进制数转换为任意进制数
url: 1616.html
id: 1616
categories:
  - C&amp;C++
  - C++学习
  - 文章页
  - 算法
date: 2019-02-08 15:23:17
tags:
---

这里采用辗转相除法来进行十进制向其他进制的转换。 辗转相除法：以一个例子来看16 转换为8进制数 16%8=0 这是最低位，然后16/8=2，2%8=2，这是次低位，依次来得到最终的结果。 代码：

#include<iostream>
#include<stack>

using namespace std;


int main(){
    stack<int> qwe;
    int C,D;
    cin>>C>>D;
    while(C!=0){
       int t = C % D;
       qwe.push(t);
       C = C / D;
    }
    while(!qwe.empty()){
        cout<<qwe.top();
        qwe.pop();
    }
    return 0;
}