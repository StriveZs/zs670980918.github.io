---
title: Pat_1044（乙级）
url: 1711.html
id: 1711
categories:
  - PAT
  - 乙级
date: 2019-03-12 18:19:26
tags:
---

1044 火星数字 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805279328157696)

火星人是以 13 进制计数的：

*   地球人的 0 被火星人称为 tret。
*   地球人数字 1 到 12 的火星文分别为：jan, feb, mar, apr, may, jun, jly, aug, sep, oct, nov, dec。
*   火星人将进位以后的 12 个高位数字分别称为：tam, hel, maa, huh, tou, kes, hei, elo, syy, lok, mer, jou。

例如地球人的数字 `29` 翻译成火星文就是 `hel mar`；而火星文 `elo nov` 对应地球数字 `115`。为了方便交流，请你编写程序实现地球和火星数字之间的互译。

### 输入格式：

输入第一行给出一个正整数 N（<100），随后 N 行，每行给出一个 \[0, 169) 区间内的数字 —— 或者是地球文，或者是火星文。

### 输出格式：

对应输入的每一行，在一行中输出翻译后的另一种语言的数字。

### 输入样例：

    4
    29
    5
    elo nov
    tam
    

### 输出样例：

    hel mar
    may
    115
    13

代码：

#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>

using namespace std;


string num1\[25\] = {"tret","jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec","tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};
string num2\[13\] = {"","tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};

//字符串变为数字
int strToNum(string s1){
    int len = s1.length();
    int num = 0;
    reverse(s1.begin(),s1.end());
    while(len > 0){
        num += (s1\[len-1\] - '0')*round(pow(10,len-1));
        len--;
    }
    return num;
}

//地球转火星
void EarthToMars(string s1){
    int temp = strToNum(s1);
    if(temp < 13){
        cout<<num1\[temp\]<<endl;
    }
    else if(temp%13 == 0){
        cout<<num2\[temp/13\]<<endl;
    }
    else{
        cout<<num2\[temp/13\]<<" "<<num1\[temp%13\]<<endl;
    }
}

//火星转地球
void MarsToEarth(string s1){
    string a\[13\] = {"###", "jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};
    string b\[13\] = {"###", "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};
    int len = s1.length();
    if(len == 3){
        for(int i=1;i<13;i++){
            if(s1 == a\[i\]){
                cout<<i<<endl;
            }
            else if(s1 == b\[i\]){
                cout<<i * 13<<endl;
            }
        }
    }else{
        int temp1=0,temp2=0;
        string t1 = s1.substr(0,3);
        string t2 = s1.substr(4,3);
        for(int i=1;i<13;i++){
            if(t1 == b\[i\]){
                temp1 = i;
            }
            if(t2 == a\[i\]){
                temp2 = i;
            }
        }
        cout<<temp1 * 13 + temp2<<endl;
    }

}

int main(){
    int num,t;
    cin>>num;
    t = num;
    string str;
    while(num > 0){
        if(t == num){
            cin.get();
        }
        getline(cin,str);
        //cout<<s1;
        if(str\[0\]>='0' && str\[0\]<='9'){
            EarthToMars(str);
        }
        else{
            MarsToEarth(str);
        }
        num--;
    }
    return 0;
}