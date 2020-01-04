---
title: Pat_1007（乙级）
url: 1633.html
id: 1633
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:56:59
tags:
  - pat
---

1007 素数对猜想 （20 分）地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805317546655744

让我们定义d​n​​为：d​n​​=p​n+1​​−p​n​​，其中p​i​​是第i个素数。显然有d​1​​=1，且对于n>1有d​n​​是偶数。“素数对猜想”认为“存在无穷多对相邻且差为2的素数”。 现给定任意正整数`N`(<10​5​​)，请计算不超过`N`的满足猜想的素数对的个数。

### 输入格式:

输入在一行给出正整数`N`。

### 输出格式:

在一行中输出不超过`N`的满足猜想的素数对的个数。

### 输入样例:

    20
    

### 输出样例:

    4

代码：
```
#include<iostream>
#include<stack>
#include<math.h>

using namespace std;

int main(){
    int n;
    bool flag = true;
    cin>>n;
    //stack<int> primeStack;
    int sum=0;
    int temp1,temp2;
    //求素数
    temp1 = 2;
    for(int i=2;i<=n;i++){
        int j=0;
        flag = true;
        for(j=2;j<=sqrt(i);j++){
            if(i%j==0){
                flag = false;
                break;
            }
        }
        if(flag && i!=2){
            //cout<<i<<" ";
            temp2 = i;
            if((temp2 - temp1) == 2){
                sum++;
            }
            temp1 = i;
            //primeStack.push(i);
        }
    }
    //cout<<endl;
    /*temp1 = primeStack.top();
    primeStack.pop();
    while(!primeStack.empty()){
        temp2 = primeStack.top();
        //cout<<temp2<<endl;
        primeStack.pop();
        if((temp1 - temp2) == 2){
            sum++;
        }
        temp1 = temp2;
    }*/
    cout<<sum<<endl;
    return 0;
}
```