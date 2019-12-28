---
title: Pat_1039（乙级）
url: 1700.html
id: 1700
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:14:34
tags:
---

1039 到底买不买 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805283241443328)

小红想买些珠子做一串自己喜欢的珠串。卖珠子的摊主有很多串五颜六色的珠串，但是不肯把任何一串拆散了卖。于是小红要你帮忙判断一下，某串珠子里是否包含了全部自己想要的珠子？如果是，那么告诉她有多少多余的珠子；如果不是，那么告诉她缺了多少珠子。 为方便起见，我们用\[0-9\]、\[a-z\]、\[A-Z\]范围内的字符来表示颜色。例如在图1中，第3串是小红想做的珠串；那么第1串可以买，因为包含了全部她想要的珠子，还多了8颗不需要的珠子；第2串不能买，因为没有黑色珠子，并且少了一颗红色的珠子。 ![figbuy.jpg](https://images.ptausercontent.com/b7e2ffa6-8819-436d-ad79-a41263abe914.jpg) 图 1

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例分别在 2 行中先后给出摊主的珠串和小红想做的珠串，两串都不超过 1000 个珠子。

### 输出格式：

如果可以买，则在一行中输出 `Yes` 以及有多少多余的珠子；如果不可以买，则在一行中输出 `No` 以及缺了多少珠子。其间以 1 个空格分隔。

### 输入样例 1：

    ppRYYGrrYBR2258
    YrR8RrY
    

### 输出样例 1：

    Yes 8
    

### 输入样例 2：

    ppRYYGrrYB225
    YrR8RrY
    

### 输出样例 2：

    No 2

代码：

#include<iostream>
#include<string.h>
#include<map>

using namespace std;

int main(){
    string s1,s2;
    map<char,int> t1;
    map<char,int> t2;
    map<char,int>::iterator pos;
    bool flag = true;
    int sum=0;
    cin>>s1>>s2;
    for(int i=0;i<s1.length();i++){
        if(t1.count(s1\[i\]) != 0){
            t1\[s1\[i\]\] += 1;
        }
        else{
            t1\[s1\[i\]\] = 1;
        }
    }
    for(int i=0;i<s2.length();i++){
        if(t2.count(s2\[i\]) != 0){
            t2\[s2\[i\]\] += 1;
        }
        else{
            t2\[s2\[i\]\] = 1;
        }
    }
    for(pos=t2.begin();pos!=t2.end();pos++){
        if(t1.count(pos->first) == 0){
            flag = false;
            break;
        }
        else{
            if(t1\[pos->first\] - pos->second < 0){
                flag = false;
                break;
            }
        }
    }
    if(flag){
        cout<<"Yes "<<s1.length()-s2.length()<<endl;
    }
    else{
        for(pos=t2.begin();pos!=t2.end();pos++){
            if(t1.count(pos->first) == 0){
                sum += pos->second;
            }
            else{
                if(t1\[pos->first\] - pos->second < 0){
                    sum += (pos->second - t1\[pos->first\]);
                }
            }
        }
        cout<<"No "<<sum<<endl;
    }
}