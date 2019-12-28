---
title: Pat_1048（乙级）
url: 1719.html
id: 1719
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:28:26
tags:
---

1048 数字加密 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805276438282240)

本题要求实现一种数字加密方法。首先固定一个加密用正整数 A，对任一正整数 B，将其每 1 位数字与 A 的对应位置上的数字进行以下运算：对奇数位，对应位的数字相加后对 13 取余——这里用 J 代表 10、Q 代表 11、K 代表 12；对偶数位，用 B 的数字减去 A 的数字，若结果为负数，则再加 10。这里令个位为第 1 位。

### 输入格式：

输入在一行中依次给出 A 和 B，均为不超过 100 位的正整数，其间以空格分隔。

### 输出格式：

在一行中输出加密后的结果。

### 输入样例：

    1234567 368782971
    

### 输出样例：

    3695Q8118

代码：

#include<iostream>
#include<string.h>
#include<algorithm>
//比较两个长度对 长度较短的那个补0
using namespace std;

int main(){
    string s1,s2,result="";
    cin>>s1>>s2;
    int cha = 0;
    if(s1.length() < s2.length()){
        cha = s2.length() - s1.length();
        string temp(cha,'0');
        s1 = temp + s1;
    }
    if(s1.length() > s2.length()){
        cha = s1.length() - s2.length();
        string temp(cha,'0');
        s2 = temp + s2;
    }

    for(int i=0;i<s2.length();i++){
        int temp1,temp2,sum;
        int j = i+1;
        if(j%2 != 0){
            temp1 = s1\[i\] - '0';
            temp2 = s2\[i\] - '0';
            sum = temp1 + temp2;
            sum = sum % 13;
            //cout<<sum<<endl;
            if(sum < 10){
                char s3 = (sum + '0');
                result = result + s3;
            }
            else if(sum == 10){
                result = result + 'J';
            }
            else if(sum == 11){
                result = result + 'Q';
            }
            else if(sum == 12){
                result = result + 'K';
            }
        }
        else{
            temp1 = s1\[i\] - '0';
            temp2 = s2\[i\] - '0';
            sum = temp2 - temp1;
            if(sum < 0){
                sum += 10;
            }
            char s3 = (sum + '0');
            result = result + s3;
        }
    }
    cout<<result<<endl;
    return 0;
}