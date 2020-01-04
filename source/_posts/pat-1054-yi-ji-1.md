---
title: Pat_1054（乙级）
url: 1731.html
id: 1731
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:38:56
tags:
  - pat
---

1054 求平均值 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805272659214336)

本题的基本要求非常简单：给定 N 个实数，计算它们的平均值。但复杂的是有些输入数据可能是非法的。一个“合法”的输入是 \[−1000,1000\] 区间内的实数，并且最多精确到小数点后 2 位。当你计算平均值的时候，不能把那些非法的数据算在内。

### 输入格式：

输入第一行给出正整数 N（≤100）。随后一行给出 N 个实数，数字间以一个空格分隔。

### 输出格式：

对每个非法输入，在一行中输出 `ERROR: X is not a legal number`，其中 `X` 是输入。最后在一行中输出结果：`The average of K numbers is Y`，其中 `K` 是合法输入的个数，`Y` 是它们的平均值，精确到小数点后 2 位。如果平均值无法计算，则用 `Undefined` 替换 `Y`。如果 `K` 为 1，则输出 `The average of 1 number is Y`。

### 输入样例 1：

    7
    5 -3.2 aaa 9999 2.3.4 7.123 2.35
    

### 输出样例 1：

    ERROR: aaa is not a legal number
    ERROR: 9999 is not a legal number
    ERROR: 2.3.4 is not a legal number
    ERROR: 7.123 is not a legal number
    The average of 3 numbers is 1.38
    

### 输入样例 2：

    2
    aaa -9999
    

### 输出样例 2：

    ERROR: aaa is not a legal number
    ERROR: -9999 is not a legal number
    The average of 0 numbers is Undefined

代码：
```
#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>
#include<cstdio>
//第三个测试点为K=1时 输出的是number而不是numbers
//第四个测试点是边界值的考察
using namespace std;

//将字符串中小数点前面的字符转换为整数
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

//将小数点后面的小数转换为小数 例如可以将213 转换为0.213
float strToPoint(string s1){
    int len = s1.length();
    float num = 0;
    int i = 0;
    while(i < len){
        num += (s1\[i\] - '0')\*pow(10,(i+1)\*-1);
        i++;
    }
    return num;
}

//判断是否每个输入的数据均为数字 小数点除外
bool IsNum(string s1){
    bool flag = true;
    for(int i=0;i<s1.length();i++){
        if(s1\[i\] < '0' || s1\[i\] > '9'){
            if(s1\[i\] != '.'){
                flag = false;
                break;
            }
        }
    }
    return flag;
}

int main(){
    int num,sum_num=0;
    double sum=0;
    cin>>num;
    for(int i=0;i<num;i++){
        int index = -1; //小数点下标
        bool fu = false; //负数标志
        bool point = false; //小数标志
        bool legal = false; //是否合法标志
        string s1,s2,front\_point,back\_point;
        cin>>s2;
        if(s2\[0\] == '-'){
            s1 = s2.substr(1,s2.length());
            fu = true;
        }
        else{
            s1 = s2;
        }
        //cout<<i<<endl;
        if(IsNum(s1)){
            //小数处理
            //cout<<count(s1.begin(),s1.end(),'.')<<endl;
            if(count(s1.begin(),s1.end(),'.') == 1){ //带小数的要考虑边界值
                //cout<<"qwe"<<endl;
                point = true;
                index = s1.find('.');
                front_point = s1.substr(0,index);
                back_point = s1.substr(index+1,s1.length()-index-1);
                if(back_point.length() <= 2){
                    int temp1 = strToNum(front_point);
                    double temp2 = strToPoint(back_point);
                    double t = temp1+temp2;
                    if(fu){
                        t = t*-1;
                    }
                    if(t>=-1000 && t<=1000){
                        sum += t;
                        sum_num++;
                        legal = true;
                    }
                }
            }
            //整数处理
            else{
                //cout<<"asd"<<endl;
                int temp = strToNum(s1);
                if(fu){
                    temp = temp * -1;
                }
                if(temp>=-1000 && temp<=1000){
                    sum += temp;
                    sum_num++;
                    legal = true;
                }
            }
        }
        if(!legal){
            cout<<"ERROR: "<<s2<<" is not a legal number"<<endl;
        }
    }
    if(sum_num == 0){
        cout<<"The average of 0 numbers is Undefined"<<endl;
    }
    else if(sum_num == 1){
        cout<<"The average of 1 number is ";
        printf("%0.2f\\n",sum);
    }
    else{
        cout<<"The average of "<<sum_num<<" numbers is ";
        printf("%0.2f\\n",double(sum/sum_num));
    }
    return 0;
}
```