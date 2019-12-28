---
title: Pat_1017（乙级）
url: 1653.html
id: 1653
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:17:50
tags:
---

1017 A除以B （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805305181847552

本题要求计算 A/B，其中 A 是不超过 1000 位的正整数，B 是 1 位正整数。你需要输出商数 Q 和余数 R，使得 A=B×Q+R 成立。

### 输入格式：

输入在一行中依次给出 A 和 B，中间以 1 空格分隔。

### 输出格式：

在一行中依次输出 Q 和 R，中间以 1 空格分隔。

### 输入样例：

    123456789050987654321 7
    

### 输出样例：

    17636684150141093474 3

代码（大数除法）：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

bool getBiggerOne(string s1,string s2){
    bool flag = false;
    if(s1.length() > s2.length()){
        return flag;
    }
    else if(s1.length() < s2.length()){
        flag = true;
        return flag;
    }
    else{
        for(int i=0;i<s1.length();i++){
            if(s1\[i\] != s2\[i\]){
                int temp1,temp2;
                temp1 = s1\[i\] - '0';
                temp2 = s2\[i\] - '0';
                if(temp1 > temp2){
                    return false;
                }
                else{
                    return true;
                }
            }
        }
    }
}

string BigNumberJian(string s1,string s2){
    if(s1 == s2){
        return "0";
    }
    string result(10000,'0');
    bool flag = getBiggerOne(s1,s2);
    if(flag){
        swap(s1,s2);
        //cout<<"3"<<endl;
    }
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    for(int i=0;i<s1.length();i++){
        result\[i\] = s1\[i\];
    }
    for(int i=0;i<s2.length();i++){
        int temp1,temp2;
        //cout<<"1"<<endl;
        temp1 = result\[i\] - '0';
        temp2 = s2\[i\] - '0';
        if(temp1 >= temp2){
            //cout<<"1"<<endl;
            result\[i\] = temp1 - temp2 + '0';
        }
        else{
            //cout<<"2"<<endl;
            result\[i+1\] = result\[i+1\] - '0' - 1 + '0';
            result\[i\] = result\[i\] - '0' + 10 - (s2\[i\]-'0') + '0';
        }
    }
    reverse(result.begin(),result.end());
    result = result.substr(result.find\_first\_not_of('0'));
    //负号判断
    if(flag){
        reverse(result.begin(),result.end());
        result += '-';
        reverse(result.begin(),result.end());
    }
    return result;
}

void BigNumberChu(){
    string s1,s2,s(10000,'0'),res;
    int len1,len2,disc;
    cin>>s1>>s2;
    if(getBiggerOne(s1,s2)){ //s1<s2 则s1/s2商为0
        cout<<"0 ";
        cout<<s1<<endl;
    }
    else{
        len1 = s1.length();
        len2 = s2.length();
        disc = len1 - len2; //记录除数和被除数之间位数之差 扩大除数disc个0
        for(int i=0;i<disc;i++){
            s2 += '0';
        }
        //cout<<s2<<endl;
        while(disc>=0){
            int sum=0;
            string temp = BigNumberJian(s1,s2);
            while(true){
                //cout<<temp<<" ";
                if(temp.find\_first\_not_of('-')){
                   break;
                }
                sum++;
                s1 = temp;
                temp = BigNumberJian(s1,s2);
            }
            //cout<<sum<<endl;
            s\[s.length()-disc-1\] = sum + '0';
            disc--;
            s2 = s2.substr(0,len2+disc);
        }
        if(s.find\_first\_not_of('0') == string::npos){
            cout<<"0 "<<s1<<endl;
        }
        else{
            string t = s.substr(s.find\_first\_not_of('0'));
            cout<<t<<" "<<s1<<endl;;
        }
    }
}

int main(){
    //cout<<BigNumberJian("22222222","22222433")<<endl;
    BigNumberChu();
    return 0;
}