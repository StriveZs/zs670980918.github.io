---
title: Pat_1005（乙级）
url: 1629.html
id: 1629
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:54:24
tags:
  - pat
---

1005 继续(3n+1)猜想 （25 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805320306507776

卡拉兹(Callatz)猜想已经在1001中给出了描述。在这个题目里，情况稍微有些复杂。 当我们验证卡拉兹猜想的时候，为了避免重复计算，可以记录下递推过程中遇到的每一个数。例如对 n=3 进行验证的时候，我们需要计算 3、5、8、4、2、1，则当我们对 n=5、8、4、2 进行验证的时候，就可以直接判定卡拉兹猜想的真伪，而不需要重复计算，因为这 4 个数已经在验证3的时候遇到过了，我们称 5、8、4、2 是被 3“覆盖”的数。我们称一个数列中的某个数 n 为“关键数”，如果 n 不能被数列中的其他数字所覆盖。 现在给定一系列待验证的数字，我们只需要验证其中的几个关键数，就可以不必再重复验证余下的数字。你的任务就是找出这些关键数字，并按从大到小的顺序输出它们。

### 输入格式：

每个测试输入包含 1 个测试用例，第 1 行给出一个正整数 K (<100)，第 2 行给出 K 个互不相同的待验证的正整数 n (1<n≤100)的值，数字间用空格隔开。

### 输出格式：

每个测试用例的输出占一行，按从大到小的顺序输出关键数字。数字间用 1 个空格隔开，但一行中最后一个数字后没有空格。

### 输入样例：

    6
    3 5 6 7 8 11
    

### 输出样例：

    7 6

代码：
```
#include<iostream>
#include<set>
#include<algorithm>
#include<string.h>
#include<stack>

using namespace std;

bool isIn(int n,set<int> a){
    set<int>::iterator pos;
    bool flag = false;
    for(pos = a.begin();pos!=a.end();pos++){
        if(*pos == n){
            flag = true;
            break;
        }
    }
    return flag;
}

int Find(int n,set<int> a){
    set<int>::iterator pos;
    int i=0;
    for(pos=a.begin();pos!=a.end();pos++){
        if(n == *pos){
            break;
        }
        i++;
    }
    return i;
}

int FindNum(int n,set<int> a){
    set<int>::iterator pos;
    int i=0;
    for(pos=a.begin();pos!=a.end();pos++){
        if(n == i){
            return *pos;
        }
        i++;
    }
}

int main(){
    set<int>::iterator pos;
    set<int> result;
    int m,sum;
    cin>>m;
    sum = m;
    set<int> qun;
    set<int> qunNumber\[m\];
    int t=0;
    while(m>0){
        int n=0;
        cin>>n;
        qun.insert(n);
        while(n != 1){
            qunNumber\[t\].insert(n);
            if(n%2 == 0){
                n = n/2;
            }
            else{
                n = (3*n+1)/2;
            }
        }
        t++;
        m--;
        /*cout<<"No."<<m<<" ";
        for(pos = linshi.begin();pos!=linshi.end();pos++){
            cout<<*pos<<" ";
        }
        cout<<endl;*/
    }
    /*for(int i=0;i<sum;i++){
        for(pos = qunNumber\[i\].begin();pos!=qunNumber\[i\].end();pos++){
            cout<<*pos<<" ";
        }
        cout<<endl;
    }*/
    /*for(pos = qun.begin();pos!=qun.end();pos++){
        cout<<*pos<<" ";
    }
    cout<<endl;*/
    int tongJi\[sum\];
    memset(tongJi,0,sum*4);
    for(int i=0;i<sum;i++){
        for(pos=qunNumber\[i\].begin();pos!=qunNumber\[i\].end();pos++){
            if(isIn(*pos,qun)){
                int t = *pos;
                int index=Find(t,qun);
                tongJi\[index\]++;
            }
        }
    }
    /*for(int i=0;i<sum;i++)
        cout<<tongJi\[i\]<<" ";
    cout<<endl;*/
    for(int i=0;i<sum;i++){
        if(tongJi\[i\] == 1){
            t=FindNum(i,qun);
            result.insert(t);
        }
    }
    /*for(pos = qun.begin();pos!=qun.end();pos++){
        cout<<*pos<<" ";
    }
    cout<<endl;*/
    stack<int> result1;
    for(pos=result.begin();pos!=result.end();pos++){
        result1.push(*pos);
    }
    while(result1.size()!=1){
        t = result1.top();
        result1.pop();
        cout<<t<<" ";
    }
    cout<<result1.top()<<endl;

    /*cout<<endl;
    for(pos = result.begin();pos!=result.end();pos++){
        cout<<*pos<<" ";
    }
    cout<<endl;*/
    return 0;
}
```