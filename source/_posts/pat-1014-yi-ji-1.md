---
title: Pat_1014（乙级）
url: 1647.html
id: 1647
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:11:25
tags:
  - pat
---

1014 福尔摩斯的约会 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805308755394560

大侦探福尔摩斯接到一张奇怪的字条：`我们约会吧！ 3485djDkxh4hhGE 2984akDfkkkkggEdsb s&hgsfdk d&Hyscvnm`。大侦探很快就明白了，字条上奇怪的乱码实际上就是约会的时间`星期四 14:04`，因为前面两字符串中第 1 对相同的大写英文字母（大小写有区分）是第 4 个字母 `D`，代表星期四；第 2 对相同的字符是 `E` ，那是第 5 个英文字母，代表一天里的第 14 个钟头（于是一天的 0 点到 23 点由数字 0 到 9、以及大写字母 `A` 到 `N` 表示）；后面两字符串第 1 对相同的英文字母 `s` 出现在第 4 个位置（从 0 开始计数）上，代表第 4 分钟。现给定两对字符串，请帮助福尔摩斯解码得到约会的时间。

### 输入格式：

输入在 4 行中分别给出 4 个非空、不包含空格、且长度不超过 60 的字符串。

### 输出格式：

在一行中输出约会的时间，格式为 `DAY HH:MM`，其中 `DAY` 是某星期的 3 字符缩写，即 `MON` 表示星期一，`TUE` 表示星期二，`WED` 表示星期三，`THU` 表示星期四，`FRI` 表示星期五，`SAT` 表示星期六，`SUN` 表示星期日。题目输入保证每个测试存在唯一解。

### 输入样例：

    3485djDkxh4hhGE 
    2984akDfkkkkggEdsb 
    s&hgsfdk 
    d&Hyscvnm
    

### 输出样例：

    THU 14:04

代码：
```
#include<iostream>
#include<string.h>

using namespace std;

string findDay(char s1){
    switch(s1){
        case 'A':return "MON";break;
        case 'B':return "TUE";break;
        case 'C':return "WED";break;
        case 'D':return "THU";break;
        case 'E':return "FRI";break;
        case 'F':return "SAT";break;
        case 'G':return "SUN";break;
    }
}

string findHour(char s1){
    switch(s1){
        case '0':return "00:";break;
        case '1':return "01:";break;
        case '2':return "02:";break;
        case '3':return "03:";break;
        case '4':return "04:";break;
        case '5':return "05:";break;
        case '6':return "06:";break;
        case '7':return "07:";break;
        case '8':return "08:";break;
        case '9':return "09:";break;
        case 'A':return "10:";break;
        case 'B':return "11:";break;
        case 'C':return "12:";break;
        case 'D':return "13:";break;
        case 'E':return "14:";break;
        case 'F':return "15:";break;
        case 'G':return "16:";break;
        case 'H':return "17:";break;
        case 'I':return "18:";break;
        case 'J':return "19:";break;
        case 'K':return "20:";break;
        case 'L':return "21:";break;
        case 'M':return "22:";break;
        case 'N':return "23:";break;
    }
}

string findMinu(int num){
    if(num>=10){
        string s1,s2,s3;
        int temp,temp1;
        temp = num%10;
        temp1 = num/10;
        s2 = temp1 + '0';
        s3 = temp + '0';
        s1 = s2 + s3;
        return s1;
    }
    else{
    switch(num){
        case 0:return "00";break;
        case 1:return "01";break;
        case 2:return "02";break;
        case 3:return "03";break;
        case 4:return "04";break;
        case 5:return "05";break;
        case 6:return "06";break;
        case 7:return "07";break;
        case 8:return "08";break;
        case 9:return "09";break;
    }
    }
}

int main(){
    string s1,s2,s3,s4,day,hour,minu;
    bool flag = false;
    cin>>s1>>s2>>s3>>s4;
    int len;
    if(s1.length()>s2.length()){
        len = s2.length();
    }
    else{
        len = s1.length();
    }
    for(int i=0;i<len;i++){
        if(s1\[i\] == s2\[i\] && s1\[i\]>='A' && s1\[i\]<='G' && flag == false){
            day = findDay(s1\[i\]);
            cout<<day<<" ";
            flag = true;
            continue;
        }
        if(flag){
          if(s1\[i\] == s2\[i\] && ((s1\[i\]>='A' && s1\[i\]<='N')||(s1\[i\]>='0' && s1\[i\]<='9'))){
            hour = findHour(s1\[i\]);
            cout<<hour;
            break;
          }
        }
    }
    if(s3.length()>s4.length()){
        len = s4.length();
    }
    else{
        len = s3.length();
    }
    for(int i=0;i<len;i++){
        if(s3\[i\] == s4\[i\] && ((s3\[i\]>='a' && s4\[i\]<='z')||(s3\[i\]>='A' && s4\[i\]<='Z'))){
            minu = findMinu(i);
            cout<<minu<<endl;
            break;
        }
    }
    return 0;
}
```