---
title: Pat_1067（乙级）
url: 1757.html
id: 1757
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:57:48
tags:
---

1067 试密码 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805266007048192)

当你试图登录某个系统却忘了密码时，系统一般只会允许你尝试有限多次，当超出允许次数时，账号就会被锁死。本题就请你实现这个小功能。

### 输入格式：

输入在第一行给出一个密码（长度不超过 20 的、不包含空格、Tab、回车的非空字符串）和一个正整数 N（≤ 10），分别是正确的密码和系统允许尝试的次数。随后每行给出一个以回车结束的非空字符串，是用户尝试输入的密码。输入保证至少有一次尝试。当读到一行只有单个 # 字符时，输入结束，并且这一行不是用户的输入。

### 输出格式：

对用户的每个输入，如果是正确的密码且尝试次数不超过 N，则在一行中输出 `Welcome in`，并结束程序；如果是错误的，则在一行中按格式输出 `Wrong password: 用户输入的错误密码`；当错误尝试达到 N 次时，再输出一行 `Account locked`，并结束程序。

### 输入样例 1：

    Correct%pw 3
    correct%pw
    Correct@PW
    whatisthepassword!
    Correct%pw
    #
    

### 输出样例 1：

    Wrong password: correct%pw
    Wrong password: Correct@PW
    Wrong password: whatisthepassword!
    Account locked
    

### 输入样例 2：

    cool@gplt 3
    coolman@gplt
    coollady@gplt
    cool@gplt
    try again
    #
    

### 输出样例 2：

    Wrong password: coolman@gplt
    Wrong password: coollady@gplt
    Welcome in

代码：

#include<iostream>
#include<string.h>
#include<deque>

using namespace std;

int main(){
    deque<string> que;
    deque<string>::iterator pos;
    string passwordR;
    int num,iter = 0;
    cin>>passwordR>>num;
    string s1="";
    cin.get(); //解决geiline提前读取一个回车的问题
    while(true){
        getline(cin,s1); //使用getline防止出现cin 无法读取的数据
        if(s1 == "#"){
            break;
        }
        que.push_back(s1);
    }
    for(pos=que.begin();pos!=que.end();pos++){
        s1 = *pos;
        if(iter < num && s1 != passwordR){
            cout<<"Wrong password: "<<s1<<endl;
            iter++;
        }
        if(iter >= num){
            cout<<"Account locked"<<endl;
            break;
        }
        if(s1 == passwordR){
            cout<<"Welcome in"<<endl;
            break;
        }
    }
    return 0;
}