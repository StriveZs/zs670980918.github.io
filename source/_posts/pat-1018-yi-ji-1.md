---
title: Pat_1018（乙级）
url: 1655.html
id: 1655
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:21:05
tags:
  - pat
---

1018 锤子剪刀布 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805304020025344

大家应该都会玩“锤子剪刀布”的游戏：两人同时给出手势，胜负规则如图所示： ![FigCJB.jpg](https://images.ptausercontent.com/724da598-b37f-4f1f-99b4-71459654ce3a.jpg) 现给出两人的交锋记录，请统计双方的胜、平、负次数，并且给出双方分别出什么手势的胜算最大。

### 输入格式：

输入第 1 行给出正整数 N（≤10​5​​），即双方交锋的次数。随后 N 行，每行给出一次交锋的信息，即甲、乙双方同时给出的的手势。`C` 代表“锤子”、`J` 代表“剪刀”、`B` 代表“布”，第 1 个字母代表甲方，第 2 个代表乙方，中间有 1 个空格。

### 输出格式：

输出第 1、2 行分别给出甲、乙的胜、平、负次数，数字间以 1 个空格分隔。第 3 行给出两个字母，分别代表甲、乙获胜次数最多的手势，中间有 1 个空格。如果解不唯一，则输出按字母序最小的解。

### 输入样例：

    10
    C J
    J B
    C B
    B B
    B C
    C C
    C B
    J B
    B C
    J J
    

### 输出样例：

    5 3 2
    2 3 5
    B B

代码（有一个测试点一直过不去）：  改正方法为应该是没有满足如果解不唯一，则输出按字母序最小的解。这个条件 所以应该采用将结果保存下来然后sort进行排序
```
#include<iostream>

using namespace std;

void zijian(int n\[\],int len){
    int t = len;
    bool flag = false;
    do{
        if((n\[t\]-1)>=0){
            n\[t\]--;
            flag = true;
        }
        else{
            n\[t\] = 9;
            t--;
        }
    }while(flag!=true);
}

bool equalZero(int n\[\],int len){
    bool flag = true;
    for(int i=0;i<len;i++){
        if(n\[i\]!=0){
            flag = false;
            break;
        }
    }
    return flag;
}

int main(){
    int num\_Jia\_C=0,num\_Jia\_J=0,num\_Jia\_B=0,num\_Yi\_C=0,num\_Yi\_J=0,num\_Yi\_B=0;
    int Jia\_Win=0,Jia\_Ping=0,Jia\_Lose=0,Yi\_Win=0,Yi\_Ping=0,Yi\_Lose=0;
    string number;
    cin>>number;
    int BigNum\[number.length()\];
    for(int i=number.length()-1;i>=0;i--){
        BigNum\[i\] = number\[i\] - '0';
    }
    // C锤子 J剪刀 B布
    while(equalZero(BigNum,number.length()) == false){
        string s1,s2;
        cin>>s1>>s2;
        if(s1\[0\] == 'C'){
            if(s2\[0\] == 'C'){
                Jia_Ping++;
                Yi_Ping++;
            }
            else if(s2\[0\] == 'B'){
                num\_Yi\_B++;
                Yi_Win++;
                Jia_Lose++;
            }
            else{
                num\_Jia\_C++;
                Yi_Lose++;
                Jia_Win++;
            }
        }
        else if(s1\[0\] == 'B'){
            if(s2\[0\] == 'C'){
                num\_Jia\_B++;
                Yi_Lose++;
                Jia_Win++;
            }
            else if(s2\[0\] == 'B'){
                Jia_Ping++;
                Yi_Ping++;
            }
            else{
                num\_Yi\_J++;
                Yi_Win++;
                Jia_Lose++;
            }
        }
        else{
            if(s2\[0\] == 'C'){
                num\_Yi\_C++;
                Yi_Win++;
                Jia_Lose++;
            }
            else if(s2\[0\] == 'B'){
                num\_Jia\_J++;
                Yi_Lose++;
                Jia_Win++;
            }
            else{
                Jia_Ping++;
                Yi_Ping++;
            }
        }
        zijian(BigNum,number.length()-1);
    }
    cout<<Jia\_Win<<" "<<Jia\_Ping<<" "<<Jia_Lose<<endl;
    cout<<Yi\_Win<<" "<<Yi\_Ping<<" "<<Yi_Lose<<endl;
    if((num\_Jia\_C >= num\_Jia\_B) && (num\_Jia\_C >= num\_Jia\_J)){
        if(num\_Jia\_B == num\_Jia\_C == num\_Jia\_J){
            cout<<"B ";
        }
        else if(num\_Jia\_B == num\_Jia\_C){
            cout<<"B ";
        }
        else{
            cout<<"C ";
        }
    }
    else if((num\_Jia\_B >= num\_Jia\_C) && (num\_Jia\_B >= num\_Jia\_J)){
        cout<<"B ";
    }
    else if((num\_Jia\_J >= num\_Jia\_C) && (num\_Jia\_J >= num\_Jia\_B)){
        if(num\_Jia\_J == num\_Jia\_C == num\_Jia\_B){
            cout<<"B ";
        }
        else if(num\_Jia\_J == num\_Jia\_B){
            cout<<"B ";
        }
        else if(num\_Jia\_J == num\_Jia\_C){
            cout<<"C ";
        }
        else{
            cout<<"J ";
        }
    }
    else{

    }

    if((num\_Yi\_C >= num\_Yi\_B) && (num\_Yi\_C >= num\_Yi\_J)){
        if(num\_Yi\_B == num\_Yi\_C == num\_Yi\_J){
            cout<<"B"<<endl;
        }
        else if(num\_Yi\_B == num\_Yi\_C){
            cout<<"B"<<endl;
        }
        else{
            cout<<"C"<<endl;
        }
    }
    else if((num\_Yi\_B >= num\_Yi\_C) && (num\_Yi\_B >= num\_Yi\_J)){
        cout<<"B"<<endl;
    }
    else if((num\_Yi\_J >= num\_Yi\_C) && (num\_Yi\_J >= num\_Yi\_B)){
        if(num\_Yi\_J == num\_Yi\_C == num\_Yi\_B){
            cout<<"B"<<endl;
        }
        else if(num\_Yi\_J == num\_Yi\_B){
            cout<<"B"<<endl;
        }
        else if(num\_Yi\_J == num\_Yi\_C){
            cout<<"C"<<endl;
        }
        else{
            cout<<"J"<<endl;
        }
    }
    else{

    }
}
```