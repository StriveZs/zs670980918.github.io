---
title: Pat_1013（乙级）
url: 1645.html
id: 1645
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:10:19
tags:
---

1013 数素数 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805309963354112

令 P​i​​ 表示第 i 个素数。现任给两个正整数 M≤N≤10​4​​，请输出 P​M​​ 到 P​N​​ 的所有素数。

### 输入格式：

输入在一行中给出 M 和 N，其间以空格分隔。

### 输出格式：

输出从 P​M​​ 到 P​N​​ 的所有素数，每 10 个数字占 1 行，其间以空格分隔，但行末不得有多余空格。

### 输入样例：

    5 27
    

### 输出样例：

    11 13 17 19 23 29 31 37 41 43
    47 53 59 61 67 71 73 79 83 89
    97 101 103

代码：

#include<iostream>
#include<math.h>

using namespace std;

int main(){
    int start,ends,sum,t=0,q=0;
    bool flag = true;
    cin>>start>>ends;
    sum = ends-start+1;
    if(start == 0){
        sum--;
    }
    for(int i=2;i<=1000000000;i++){
        int j=0;
        flag = true;
        for(j=2;j<=sqrt(i);j++){
            if(i%j==0){
                flag = false;
                break;
            }
        }
        if(sum == 0){
            break;
        }
        if(flag == true){
            t++;
            if(t>=start){
                if(sum==1){
                    cout<<i<<endl;
                    break;
                }
                q++;
                sum--;
                if(q%10!=0){
                    cout<<i<<" ";
                }
                else{
                    cout<<i<<endl;
                }
            }
        }
    }
    return 0;
}