---
title: Pat_1027（乙级）
url: 1674.html
id: 1674
categories:
  - PAT
  - 乙级
date: 2019-03-12 11:38:52
tags:
---

1027 打印沙漏 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805294251491328)

本题要求你写个程序把给定的符号打印成沙漏的形状。例如给定17个“*”，要求按下列格式打印

    *****
     ***
      *
     ***
    *****
    

所谓“沙漏形状”，是指每行输出奇数个符号；各行符号中心对齐；相邻两行符号数差2；符号数先从大到小顺序递减到1，再从小到大顺序递增；首尾符号数相等。 给定任意N个符号，不一定能正好组成一个沙漏。要求打印出的沙漏能用掉尽可能多的符号。

### 输入格式:

输入在一行给出1个正整数N（≤1000）和一个符号，中间以空格分隔。

### 输出格式:

首先打印出由给定符号组成的最大的沙漏形状，最后在一行中输出剩下没用掉的符号数。

### 输入样例:

    19 *
    

### 输出样例:

    *****
     ***
      *
     ***
    *****
    2

代码：

#include<iostream>
#include<string.h>

using namespace std;

int main(){
    int num,maxnum,sum=0,temp = 1;
    char te;
    cin>>num>>te;
    if(num == 0){
        cout<<num;
    }
    else{
        num -= temp;
        if(num == 0){
            cout<<te<<endl;
            cout<<num<<endl;
            return 0;
        }
        while(num > 0){
            temp = temp + 2;
            num -= 2*temp;
        }
        if(num < 0){
            num += temp*2;
            temp -= 2;
            sum = num;
            num = 0;
        }
        //cout<<num<<" "<<temp<<endl;
        if(num == 0){
            maxnum = temp; //最大个数的*
            string s1(temp,te);
            int flag1 = 0;
            cout<<s1<<endl;
            if(temp >= 3){
            temp = temp - 2;
            while(temp != maxnum){
                int n = maxnum - temp;
                string s1(temp,te);
                string s2(n/2,' ');
                cout<<s2+s1+s2<<endl;
                if(flag1 == 0){
                    temp = temp - 2;
                    if(temp == 1){
                        flag1 = 1;
                    }
                }
                else{
                    temp = temp + 2;
                }
            }
            string s3(maxnum,te);
            cout<<s3<<endl;
            }
        }
        cout<<sum;
    }
    return 0;
}