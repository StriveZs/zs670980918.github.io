---
title: Pat_1002（乙级）
url: 1623.html
id: 1623
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:47:08
tags:
  - pat
---

1002 写出这个数 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805324509200384

读入一个正整数 n，计算其各位数字之和，用汉语拼音写出和的每一位数字。

### 输入格式：

每个测试输入包含 1 个测试用例，即给出自然数 n 的值。这里保证 n 小于 10​100​​。

### 输出格式：

在一行内输出 n 的各位数字之和的每一位，拼音数字间有 1 空格，但一行中最后一个拼音数字后没有空格。

### 输入样例：

    1234567890987654321123456789
    

### 输出样例：

    yi san wu

代码：
```
#include<iostream>
#include<string>
#include<math.h>

using namespace std;
void search_name(int temp){
    switch(temp){
        case 0:cout<<"ling";break;
        case 1:cout<<"yi";break;
        case 2:cout<<"er";break;
        case 3:cout<<"san";break;
        case 4:cout<<"si";break;
        case 5:cout<<"wu";break;
        case 6:cout<<"liu";break;
        case 7:cout<<"qi";break;
        case 8:cout<<"ba";break;
        case 9:cout<<"jiu";break;
    }
}

int pow10(int i){
    int m=1;
    while(i!=0){
        m = m*10;
        i--;
    }
    return m;
}

int main(){
    string st1;
    cin>>st1;
    int sum = 0,temp,mess,t,m;
    for(int i = 0;i<st1.length();i++){
        sum += st1\[i\] - '0';
    }
    temp = sum/10;
    if(temp == 0){
        temp = sum%10;
        search_name(temp);
    }
    else{
        //cout<<sum<<endl;
        temp = sum;
        mess=0;
        while(temp != 0){
            temp = temp/10;
            mess++;
        }
        //cout<<mess<<endl;
        for(int i=mess-1;i>=0;i--){
            m = pow10(i);
            //cout<<m<<endl;
            if(i==0){
                search_name(sum);
            }
            else{
                t = sum/m;
                search_name(t);
                cout<<" ";
                sum -= (m*t);
                //cout<<sum<<endl;
            }
        }
    }
    return 0;
}
```