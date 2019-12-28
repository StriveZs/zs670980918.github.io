---
title: Pat_1074（乙级）
url: 1772.html
id: 1772
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:09:50
tags:
---

1074 宇宙无敌加法器 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805263297527808)

地球人习惯使用十进制数，并且默认一个数字的每一位都是十进制的。而在 PAT 星人开挂的世界里，每个数字的每一位都是不同进制的，这种神奇的数字称为“PAT数”。每个 PAT 星人都必须熟记各位数字的进制表，例如“……0527”就表示最低位是 7 进制数、第 2 位是 2 进制数、第 3 位是 5 进制数、第 4 位是 10 进制数，等等。每一位的进制 d 或者是 0（表示十进制）、或者是 \[2，9\] 区间内的整数。理论上这个进制表应该包含无穷多位数字，但从实际应用出发，PAT 星人通常只需要记住前 20 位就够用了，以后各位默认为 10 进制。 在这样的数字系统中，即使是简单的加法运算也变得不简单。例如对应进制表“0527”，该如何计算“6203 + 415”呢？我们得首先计算最低位：3 + 5 = 8；因为最低位是 7 进制的，所以我们得到 1 和 1 个进位。第 2 位是：0 + 1 + 1（进位）= 2；因为此位是 2 进制的，所以我们得到 0 和 1 个进位。第 3 位是：2 + 4 + 1（进位）= 7；因为此位是 5 进制的，所以我们得到 2 和 1 个进位。第 4 位是：6 + 1（进位）= 7；因为此位是 10 进制的，所以我们就得到 7。最后我们得到：6203 + 415 = 7201。

### 输入格式：

输入首先在第一行给出一个 N 位的进制表（0 < N ≤ 20），以回车结束。 随后两行，每行给出一个不超过 N 位的非负的 PAT 数。

### 输出格式：

在一行中输出两个 PAT 数之和。

### 输入样例：

    30527
    06203
    415
    

### 输出样例：

    7201

代码：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

int main(){
    string pat,num1,num2,result="";
    cin>>pat>>num1>>num2;
    int num;
    num = pat.length() - num1.length();
    string tt(num,'0');
    num1 = tt + num1;
    num = pat.length() - num2.length();
    string tt1(num,'0');
    num2 = tt1 + num2;
    reverse(pat.begin(),pat.end());
    reverse(num1.begin(),num1.end());
    reverse(num2.begin(),num2.end());
    int flag = 0; //进位标志
    for(int i=0;i<num1.length();i++){
        int jinzhi;
        if(pat\[i\] == 'd'){
            jinzhi = 0;
        }
        else{
            jinzhi = pat\[i\] - '0';
        }
        int t1,t2;
        t1 = num1\[i\] - '0';
        t2 = num2\[i\] - '0';
        if(jinzhi == 0){
            jinzhi = 10;
            result += (((t1+t2+flag)%jinzhi) + '0');
            flag = (t1+t2+flag)/jinzhi;
        }
        else{
            result += (((t1+t2+flag)%jinzhi) + '0');
            flag = (t1+t2+flag)/jinzhi;
        }
    }
    if(flag != 0){
        result += (flag + '0'); //特别处理如果大于进制表的位数 则对进位的数据按照十进制来添加到头
    }
    reverse(result.begin(),result.end());
    if(result.find\_first\_not_of('0') == string::npos){
        cout<<0<<endl;
    }
    else{
        cout<<result.substr(result.find\_first\_not_of('0'),result.length())<<endl;
    }
    return 0;
}