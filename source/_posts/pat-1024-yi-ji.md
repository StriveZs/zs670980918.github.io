---
title: Pat_1024（乙级）
url: 1667.html
id: 1667
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:34:50
tags:
---

1024 科学计数法 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805297229447168)

科学计数法是科学家用来表示很大或很小的数字的一种方便的方法，其满足正则表达式 \[+-\]\[1-9\]`.`\[0-9\]+E\[+-\]\[0-9\]+，即数字的整数部分只有 1 位，小数部分至少有 1 位，该数字及其指数部分的正负号即使对正数也必定明确给出。 现以科学计数法的格式给出实数 A，请编写程序按普通数字表示法输出 A，并保证所有有效位都被保留。

### 输入格式：

每个输入包含 1 个测试用例，即一个以科学计数法表示的实数 A。该数字的存储长度不超过 9999 字节，且其指数的绝对值不超过 9999。

### 输出格式：

对每个测试用例，在一行中按普通数字表示法输出 A，并保证所有有效位都被保留，包括末尾的 0。

### 输入样例 1：

    +1.23400E-03
    

### 输出样例 1：

    0.00123400
    

### 输入样例 2：

    -1.2E+10
    

### 输出样例 2：

    -12000000000

代码:

#include<iostream>
#include<string.h>
#include<math.h>

using namespace std;

int main(){
    string s1,s3,qwe;
    cin>>s1;
    int pointBack,flag = 0,flag1=0;
    pointBack = 0; //小数点后面的位数
    qwe += s1\[0\];
    qwe += s1\[1\];
    for(int i=2;i<s1.length();i++){
        if(s1\[i\] == '.'){
            flag = 1;
            continue;
        }
        if(s1\[i\] == 'E'){
            flag = 0;
            flag1 = 1;
            continue;
        }
        if(flag == 1){
            pointBack++;
            qwe += s1\[i\];
        }
        if(flag1 == 1){
            s3 += s1\[i\];
        }
    }
    //cout<<qwe<<" "<<s3<<endl;
    int a,b,sum = 0;
    char t = s3\[0\];
    s3\[0\] = '0';
    int index = s3.find\_first\_not_of('0');
    s3\[0\] = t;
    //cout<<index<<endl;
    for(int i=index;i<s3.length();i++){
        a = s3\[i\] - '0';
        b = round(pow(10,s3.length()-1-i));
        sum += (a*b);
        //cout<<a<<" "<<b<<" "<<sum<<endl;
    }
    //cout<<qwe<<" "<<s3<<endl;
    if(s3\[0\] == '-'){
        //cout<<"qqwe"<<endl;
        string temp(sum,'0'),result;
        //cout<<sum<<endl;
        if(qwe\[0\] == '-'){
            qwe = qwe\[0\] + temp + qwe.substr(1,qwe.length());
            result = qwe.substr(0,2) + '.' + qwe.substr(2,qwe.length());
        }
        else{
            qwe = temp + qwe.substr(1,qwe.length());
            result = qwe.substr(0,1) + '.' + qwe.substr(1,qwe.length());
        }
        cout<<result<<endl;
    }
    else{
        string result;
        if(sum > pointBack){
            string temp1(sum-pointBack,'0');
            result = qwe + temp1;
        }
        else if(sum == pointBack){
            result = qwe;
        }
        else{
            //cout<<sum<<" "<<pointBack<<endl;
            result = qwe.substr(0,sum+2) + '.' + qwe.substr(sum+2,qwe.length());
        }
        if(qwe\[0\] == '+'){
            result = result.substr(1,result.length());
        }
        cout<<result<<endl;
    }
    return 0;
}