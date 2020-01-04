---
title: Pat_1086（乙级）
url: 1796.html
id: 1796
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:28:08
tags:
 - pat
---

1086 就不告诉你 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1038429065476579328)

做作业的时候，邻座的小盆友问你：“五乘以七等于多少？”你应该不失礼貌地围笑着告诉他：“五十三。”本题就要求你，对任何一对给定的正整数，倒着输出它们的乘积。 ![53.jpg](https://images.ptausercontent.com/0c3a4497-27c3-45ea-9c8e-5a1ab2df48af.jpg)

### 输入格式：

输入在第一行给出两个不超过 1000 的正整数 A 和 B，其间以空格分隔。

### 输出格式：

在一行中倒着输出 A 和 B 的乘积。

### 输入样例：

    5 7
    

### 输出样例：

    53

代码：
```
#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

string BigNumberMult(){
    string s1,s2,s(10000,'0');
    cin>>s1>>s2;
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    for(int i=0;i<s1.length();i++){
        for(int j=0;j<s2.length();j++){
            int temp = (s1\[i\] - '0') * (s2\[j\] - '0');
            s\[i+j+1\] = s\[i+j+1\] - '0' + (s\[i+j\] - '0' + temp) / 10 + '0';
            s\[i+j\] = (s\[i+j\] - '0' + temp) % 10 + '0';
        }
    }
    reverse(s.begin(),s.end());
    if(s.find\_first\_not_of('0') == string::npos){
        return "0";
    }
    else{
        return s.substr(s.find\_first\_not_of('0'));
    }
}

int main(){
    string result;
    result = BigNumberMult();
    reverse(result.begin(),result.end());
    cout<<result.substr(result.find\_first\_not_of('0'))<<endl; //对于 10 * 10 得到的100 要将001处理为1
    return 0;
}
```