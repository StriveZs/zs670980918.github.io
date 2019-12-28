---
title: Pat_1031（乙级）
url: 1682.html
id: 1682
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:45:40
tags:
---

1031 查验身份证 （15 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805290334011392)

一个合法的身份证号码由17位地区、日期编号和顺序编号加1位校验码组成。校验码的计算规则如下： 首先对前17位数字加权求和，权重分配为：{7，9，10，5，8，4，2，1，6，3，7，9，10，5，8，4，2}；然后将计算的和对11取模得到值`Z`；最后按照以下关系对应`Z`值与校验码`M`的值：

    Z：0 1 2 3 4 5 6 7 8 9 10
    M：1 0 X 9 8 7 6 5 4 3 2
    

现在给定一些身份证号码，请你验证校验码的有效性，并输出有问题的号码。

### 输入格式：

输入第一行给出正整数N（≤100）是输入的身份证号码的个数。随后N行，每行给出1个18位身份证号码。

### 输出格式：

按照输入的顺序每行输出1个有问题的身份证号码。这里并不检验前17位是否合理，只检查前17位是否全为数字且最后1位校验码计算准确。如果所有号码都正常，则输出`All passed`。

### 输入样例1：

    4
    320124198808240056
    12010X198901011234
    110108196711301866
    37070419881216001X
    

### 输出样例1：

    12010X198901011234
    110108196711301866
    37070419881216001X
    

### 输入样例2：

    2
    320124198808240056
    110108196711301862
    

### 输出样例2：

    All passed

代码：

#include<iostream>
#include<map>
#include<string.h>

using namespace std;

int main(){
    map<int,char> dir;
    dir\[0\] = '1';
    dir\[1\] = '0';
    dir\[2\] = 'X';
    dir\[3\] = '9';
    dir\[4\] = '8';
    dir\[5\] = '7';
    dir\[6\] = '6';
    dir\[7\] = '5';
    dir\[8\] = '4';
    dir\[9\] = '3';
    dir\[10\] = '2';
    int quan\[17\] = {7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
    int num;
    cin>>num;
    bool flag = true;
    string str\[num\];
    for(int i=0;i<num;i++){
        cin>>str\[i\];
    }
    for(int i=0;i<num;i++){
        int temp1,sum = 0;
        char temp;
        for(int j=0;j<17;j++){
            temp = str\[i\]\[j\];
            if(temp == 'X'){
                sum = sum + quan\[j\]*10;
            }
            else{
                sum = sum + quan\[j\]*(temp-'0');
            }
        }
        sum = sum%11;
        //cout<<sum<<endl;
        temp = str\[i\]\[17\];
        if(temp == 'X'){
            temp1 = 'X';
        }
        else{
            temp1 = temp;
        }
        if(dir\[sum\] != temp1){
            flag = false;
            cout<<str\[i\]<<endl;
        }
     }
     if(flag){
        cout<<"All passed"<<endl;
     }
    return 0;
}