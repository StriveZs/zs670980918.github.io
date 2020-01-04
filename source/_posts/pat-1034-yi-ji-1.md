---
title: Pat_1034（乙级）
url: 1688.html
id: 1688
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:50:54
tags:
  - pat
---

1034 有理数四则运算 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805287624491008)

本题要求编写程序，计算 2 个有理数的和、差、积、商。

### 输入格式：

输入在一行中按照 `a1/b1 a2/b2` 的格式给出两个分数形式的有理数，其中分子和分母全是整型范围内的整数，负号只可能出现在分子前，分母不为 0。

### 输出格式：

分别在 4 行中按照 `有理数1 运算符 有理数2 = 结果` 的格式顺序输出 2 个有理数的和、差、积、商。注意输出的每个有理数必须是该有理数的最简形式 `k a/b`，其中 `k` 是整数部分，`a/b` 是最简分数部分；若为负数，则须加括号；若除法分母为 0，则输出 `Inf`。题目保证正确的输出中没有超过整型范围的整数。

### 输入样例 1：

    2/3 -4/2
    

### 输出样例 1：

    2/3 + (-2) = (-1 1/3)
    2/3 - (-2) = 2 2/3
    2/3 * (-2) = (-1 1/3)
    2/3 / (-2) = (-1/3)
    

### 输入样例 2：

    5/3 0/6
    

### 输出样例 2：

    1 2/3 + 0 = 1 2/3
    1 2/3 - 0 = 1 2/3
    1 2/3 * 0 = 0
    1 2/3 / 0 = Inf

代码：（复杂版本）
```
//以下版本实现实在是太复杂了 所以不采用了
#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>

using namespace std;

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

void numberOper(string s1,string s2,bool flag1,bool flag2){
    int index1 = s1.find('/');
    int index2 = s2.find('/');
    int q1\_front,q1\_back,q2\_front,q2\_back;
    int s1\_front,s1\_back,s2\_front,s2\_back;
    if(flag1){
        s1_front = strToNum(s1.substr(1,index1-1));
    }
    else{
        s1_front = strToNum(s1.substr(0,index1));
    }
    s1_back = strToNum(s1.substr(index1+1,s1.length()));
    if(flag2){
        s2_front = strToNum(s2.substr(1,index2-1));
    }
    else{
        s2_front = strToNum(s2.substr(0,index2));
    }
    s2_back = strToNum(s2.substr(index2+1,s2.length()));
    //cout<<s1\_front<<" "<<s1\_back<<endl;
    //cout<<s2\_front<<" "<<s2\_back<<endl;
    int fenmu = s2\_back * s1\_back;
    int s1\_fenzi = s1\_front * s2_back;
    int s2\_fenzi = s2\_front * s1_back;
    if(flag1){
        s1\_fenzi = s1\_fenzi * -1;
    }
    if(flag2){
        s2\_fenzi = s2\_fenzi * -1;
    }
    cout<<flag1<<flag2<<s1\_fenzi<<" "<<s2\_fenzi<<endl;
    int fenzi = s1\_fenzi + s2\_fenzi;
    bool flag3 = false;
    if(fenzi < 0){
        flag3 = true;
        fenzi = 0 - fenzi;
    }
    int jinwei = 0,yuwei = -1;
    jinwei = fenzi/fenmu;
    if(jinwei != 0){
        yuwei = fenzi%fenmu;
        fenzi = yuwei;
    }
    //cout<<fenzi<<endl;
    if(fenmu%fenzi == 0){
        fenmu = fenmu/fenzi;
        fenzi = 1;
    }
    if(jinwei == 0){
       cout<<fenzi<<"/"<<fenmu<<endl;
    }
    else{
        if(flag3){
            cout<<"-";
            cout<<jinwei<<" "<<fenzi<<"/"<<fenmu<<endl;
        }
    }
}

int main(){
    string s1,s2;
    cin>>s1>>s2;
    bool flag1=false,flag2=false; //正负标志
    if(s1\[0\] == '-'){
        flag1 = true;
    }
    if(s2\[0\] == '-'){
        flag2 = true;
    }
    numberOper(s1,s2,flag1,flag2);
    return 0;
}
```
由于上面的版本太过复杂所以不在采用了，下面是优化版本 代码：
```
#include<iostream>
#include<cstdio>

using namespace std;

//求两个数的最大公约数
long int huajian(long int a,long int b){
    if(b == 0){
        return a;
    }
    else{
        return huajian(b,a%b);
    }
}

//化简函数
void simplf(long int fronts,long int backs){
    bool flag = false;//是否为负数的分子判断
    long int jinwei=0,yushu=-1;
    if(backs == 0){
        cout<<"Inf";
    }
    else if(fronts == 0){
        cout<<"0";
    }
    else{
        if(fronts < 0){
            flag = true;
            fronts = 0 - fronts;
        }
        if(fronts > backs){
            jinwei = fronts / backs;
            yushu = fronts % backs;
            fronts = yushu;
        }
        long int gcd = huajian(fronts,backs);
        fronts = fronts / gcd;
        backs = backs / gcd;
        if(flag){
            cout<<"(-";
        }
        if(jinwei != 0){
            if(fronts == 0){
                cout<<jinwei;
            }
            else{
                cout<<jinwei<<" ";
            }
        }
        if(fronts != 0){
            cout<<fronts<<"/"<<backs;
        }
        if(flag){
            cout<<")";
        }
    }
}
int main(){
    long int t1\_front,t1\_back,t2\_front,t2\_back,result\_front,result\_back;
    scanf("%ld/%ld %ld/%ld",&t1\_front,&t1\_back,&t2\_front,&t2\_back);
    //加法
    result\_front = t1\_front * t2\_back + t2\_front * t1_back;
    result\_back = t2\_back * t1_back;
    simplf(t1\_front,t1\_back);cout<<" + ";simplf(t2\_front,t2\_back);cout<<" = ";simplf(result\_front,result\_back);cout<<endl;
    //减法
    result\_front = t1\_front * t2\_back - t2\_front * t1_back;
    result\_back = t2\_back * t1_back;
    simplf(t1\_front,t1\_back);cout<<" - ";simplf(t2\_front,t2\_back);cout<<" = ";simplf(result\_front,result\_back);cout<<endl;
    //乘法
    result\_front = t1\_front * t2_front;
    result\_back = t2\_back * t1_back;
    simplf(t1\_front,t1\_back);cout<<" * ";simplf(t2\_front,t2\_back);cout<<" = ";simplf(result\_front,result\_back);cout<<endl;
    //除法
    bool flag = false;
    if(t2_front<0){
        flag = true;
        t2\_front = 0 - t2\_front;
        t2\_back = t2\_back * -1;
    }
    result\_front = t1\_front * t2_back;
    result\_back = t1\_back * t2_front;
    if(flag){
        t2\_back = 0 - t2\_back;
        t2\_front = t2\_front * -1;
    }
    simplf(t1\_front,t1\_back);cout<<" / ";simplf(t2\_front,t2\_back);cout<<" = ";simplf(result\_front,result\_back);cout<<endl;
    return 0;
}
```