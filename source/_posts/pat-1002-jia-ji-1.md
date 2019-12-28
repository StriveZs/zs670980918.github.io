---
title: Pat_1002（甲级）
url: 1819.html
id: 1819
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-25 23:22:13
tags:
---

1002 A+B for Polynomials （25 分) [原文地址](https://pintia.cn/problem-sets/994805342720868352/problems/994805526272000000)

This time, you are supposed to find A+B where A and B are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial: K N​1​​ a​N​1​​​​ N​2​​ a​N​2​​​​ ... N​K​​ a​N​K​​​​ where K is the number of nonzero terms in the polynomial, N​i​​ and a​N​i​​​​ (i=1,2,⋯,K) are the exponents and coefficients, respectively. It is given that 1≤K≤10，0≤N​K​​<⋯<N​2​​<N​1​​≤1000.

### Output Specification:

For each test case you should output the sum of A and B in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate to 1 decimal place.

### Sample Input:

    2 1 2.4 0 3.2
    2 2 1.5 1 0.5
    

### Sample Output:

    3 2 1.5 1 2.9 0 3.2

代码：

#include<iostream>
#include<map>
#include<cstdio>
#include<vector>
#include<algorithm>

//这里面不需要输出系数为0的
using namespace std;

struct Plot{
    int exponents; //指数
    float coefficients; //系数
};

bool cmp(Plot a,Plot b){
    return a.exponents > b.exponents;
}

int main(){
    vector<Plot> list1;
    vector<Plot>::iterator poss;
    map<int,float> Ploy;
    map<int,float>::iterator pos;
    int K1,K2,sum=0;
    cin>>K1;
    for(int i=0;i<K1;i++){
        int t1;
        float t2;
        cin>>t1>>t2;
        if(Ploy.count(t1) == 0){
            Ploy\[t1\] = t2;
        }
        else{
            Ploy\[t1\] += t2;
        }
    }
    cin>>K2;
    for(int i=0;i<K2;i++){
        int t1;
        float t2;
        cin>>t1>>t2;
        if(Ploy.count(t1) == 0){
            Ploy\[t1\] = t2;
        }
        else{
            Ploy\[t1\] += t2;
        }
    }
    for(pos=Ploy.begin();pos!=Ploy.end();pos++){
        if((*pos).second != 0){
            Plot tt;
            tt.exponents = (*pos).first;
            tt.coefficients = (*pos).second;
            sum++;
            list1.push_back(tt);
        }
    }
    sort(list1.begin(),list1.end(),cmp);
    cout<<sum;
    for(poss=list1.begin();poss!=list1.end();poss++){
        printf(" %d %.1f",(\*poss).exponents,(\*poss).coefficients);
    }
    /*
    if(sum != 1 && sum != 0){
        pos = --Ploy.end();
        for(;pos!=Ploy.begin();pos--){
            printf(" %d %.1f",(\*pos).first,(\*pos).second);
        }
        pos = Ploy.begin();
        printf(" %d %.1f",(\*pos).first,(\*pos).second);
        cout<<endl;
    }
    else if(sum == 1){
        pos = Ploy.begin();
        printf(" %d %.1f",(\*pos).first,(\*pos).second);
        cout<<endl;
    }*/
    return 0;
}