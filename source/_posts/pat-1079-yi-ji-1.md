---
title: Pat_1079（乙级）
url: 1782.html
id: 1782
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:17:29
tags:
 - pat
---

1079 延迟的回文数 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805261754023936)

给定一个 k+1 位的正整数 N，写成 a​k​​⋯a​1​​a​0​​ 的形式，其中对所有 i 有 0≤a​i​​<10 且 a​k​​>0。N 被称为一个**回文数**，当且仅当对所有 i 有 a​i​​=a​k−i​​。零也被定义为一个回文数。 非回文数也可以通过一系列操作变出回文数。首先将该数字逆转，再将逆转数与该数相加，如果和还不是一个回文数，就重复这个逆转再相加的操作，直到一个回文数出现。如果一个非回文数可以变出回文数，就称这个数为**延迟的回文数**。（定义翻译自 [https://en.wikipedia.org/wiki/Palindromic_number](https://en.wikipedia.org/wiki/Palindromic_number) ） 给定任意一个正整数，本题要求你找到其变出的那个回文数。

### 输入格式：

输入在一行中给出一个不超过1000位的正整数。

### 输出格式：

对给定的整数，一行一行输出其变出回文数的过程。每行格式如下

    A + B = C
    

其中 `A` 是原始的数字，`B` 是 `A` 的逆转数，`C` 是它们的和。`A` 从输入的整数开始。重复操作直到 `C` 在 10 步以内变成回文数，这时在一行中输出 `C is a palindromic number.`；或者如果 10 步都没能得到回文数，最后就在一行中输出 `Not found in 10 iterations.`。

### 输入样例 1：

    97152
    

### 输出样例 1：

    97152 + 25179 = 122331
    122331 + 133221 = 255552
    255552 is a palindromic number.
    

### 输入样例 2：

    196
    

### 输出样例 2：

    196 + 691 = 887
    887 + 788 = 1675
    1675 + 5761 = 7436
    7436 + 6347 = 13783
    13783 + 38731 = 52514
    52514 + 41525 = 94039
    94039 + 93049 = 187088
    187088 + 880781 = 1067869
    1067869 + 9687601 = 10755470
    10755470 + 07455701 = 18211171
    Not found in 10 iterations.

代码：
```
#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>

using namespace std;
//这里采用大数加法 如果使用普通的加法的话 会出现超过范围的数值无法解决
string BigNumberAdd(string s1,string s2){
    string result(10000,'0');
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    for(int i=0;i<s1.length();i++){
        result\[i\] = s1\[i\];
    }
    int temp = 0;
    for(int i=0;i<s2.length();i++){
        temp += (result\[i\]-'0' + s2\[i\] -'0');
        result\[i\] = temp%10 + '0';
        temp /= 10;
    }
    result\[s2.length()\] = (result\[s2.length()\]-'0') + temp + '0';
    reverse(result.begin(),result.end());
    return result.substr(result.find\_first\_not_of('0'));
}

bool IsPalindromic_Number(string s1){
    bool flag = true;
    if(s1 == "0"){
        return flag;
    }
    else{
        for(int i=0;i<s1.length()/2;i++){
            if(s1\[i\] != s1\[s1.length() - i -1\]){
                flag = false;
                break;
            }
        }
    }
    return flag;
}

int main(){
    string number;
    int iter = 0; //计数器
    cin>>number;
    if(IsPalindromic_Number(number)){
        cout<<number<<" is a palindromic number."<<endl;
    }
    else{
        while(!IsPalindromic_Number(number) && iter < 10){
            string t1 = number;
            reverse(t1.begin(),t1.end());
            string temp = BigNumberAdd(number,t1);
            cout<<number<<" + "<<t1<<" = "<<temp<<endl;
            number = temp;
            iter++;
        }
        if(iter == 10){
            cout<<"Not found in 10 iterations."<<endl;
        }
        else{
            cout<<number<<" is a palindromic number."<<endl;
        }
    }
    return 0;
}
```