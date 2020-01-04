---
title: Pat_1075（乙级）
url: 1774.html
id: 1774
categories:
  - PAT
  - 文章页
date: 2019-03-18 11:13:04
tags:
  - pat
---

1075 链表元素分类 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805262953594880)

给定一个单链表，请编写程序将链表元素进行分类排列，使得所有负值元素都排在非负值元素的前面，而 \[0, K\] 区间内的元素都排在大于 K 的元素前面。但每一类内部元素的顺序是不能改变的。例如：给定链表为 18→7→-4→0→5→-6→10→11→-2，K 为 10，则输出应该为 -4→-6→-2→7→0→5→10→18→11。

### 输入格式：

每个输入包含一个测试用例。每个测试用例第 1 行给出：第 1 个结点的地址；结点总个数，即正整数N (≤10​5​​)；以及正整数K (≤10​3​​)。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。 接下来有 N 行，每行格式为：

    Address Data Next
    

其中 `Address` 是结点地址；`Data` 是该结点保存的数据，为 \[−10​5​​,10​5​​\] 区间内的整数；`Next` 是下一结点的地址。题目保证给出的链表不为空。

### 输出格式：

对每个测试用例，按链表从头到尾的顺序输出重排后的结果链表，其上每个结点占一行，格式与输入相同。

### 输入样例：

    00100 9 10
    23333 10 27777
    00000 0 99999
    00100 18 12309
    68237 -6 23333
    33218 -4 00000
    48652 -2 -1
    99999 5 68237
    27777 11 48652
    12309 7 33218
    

### 输出样例：

    33218 -4 68237
    68237 -6 48652
    48652 -2 12309
    12309 7 00000
    00000 0 99999
    99999 5 23333
    23333 10 00100
    00100 18 27777
    27777 11 -1

代码（两个测试点通过不了的版本）：
```
#include<iostream>
#include<string.h>
#include<algorithm>
#include<vector>

using namespace std;

struct Node{
    string Address;
    int Data;
    string Next;
};

void sorted(Node nodes\[\],int num){
    string s1,s2;
    int t;
    for(int i=0;i<num-1;i++){
        for(int j = i+1;j<num;j++){
            if(nodes\[i\].Next == nodes\[j\].Address){
                swap(nodes\[j\],nodes\[i+1\]);
            }
        }
    }
}

int main(){
    vector<Node> que1; //小于0
    vector<Node> que2; //大于等于0 小于等于K
    vector<Node> que3; //大于K
    vector<Node>::iterator pos;
    string start;
    int num,K;
    cin>>start>>num>>K;
    Node nodes\[num\];
    for(int i=0;i<num;i++){
        cin>>nodes\[i\].Address>>nodes\[i\].Data>>nodes\[i\].Next;
        if(nodes\[i\].Address == start && i != 0){
            swap(nodes\[0\],nodes\[i\]);
        }
    }
    sorted(nodes,num);
    /*cout<<endl;
    for(int i=0;i<num;i++){
        cout<<nodes\[i\].Address<<" "<<nodes\[i\].Data<<" "<<nodes\[i\].Next<<endl;
    }
    cout<<endl;*/
    for(int i=0;i<num;i++){
        if(nodes\[i\].Data < 0){
            que1.push_back(nodes\[i\]);
        }
        else if(nodes\[i\].Data >= 0 && nodes\[i\].Data <= K){
            que2.push_back(nodes\[i\]);
        }
        else{
            que3.push_back(nodes\[i\]);
        }
    }
    if(!que1.empty()){
        for(pos=que1.begin();pos != que1.end();pos++){
            if(pos != que1.end()-1){
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" "<<(*(pos+1)).Address<<endl;
            }
            else{
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" ";
            }
        }
        if(!que2.empty()){
            cout<<(*que2.begin()).Address<<endl;
        }
        else if(!que3.empty()){
            cout<<(*que3.begin()).Address<<endl;
        }
        else{
            cout<<"-1"<<endl;
        }
    }
    if(!que2.empty()){
        for(pos=que2.begin();pos != que2.end();pos++){
            if(pos != que2.end()-1){
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" "<<(*(pos+1)).Address<<endl;
            }
            else{
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" ";
            }
        }
        if(!que3.empty()){
            cout<<(*que3.begin()).Address<<endl;
        }
        else{
            cout<<"-1"<<endl;
        }
    }
    if(!que3.empty()){
        for(pos=que3.begin();pos != que3.end();pos++){
            if(pos != que3.end()-1){
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" "<<(*(pos+1)).Address<<endl;
            }
            else{
                cout<<(\*pos).Address<<" "<<(\*pos).Data<<" ";
            }
        }
        cout<<"-1"<<endl;
    }
    return 0;
}
```
改正后版本：
```
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e6 + 10;
int st, N, K;

struct Node{
    int address;
    int val;
    int nx;
};

Node n;
vector<Node> l;
vector<Node> ans;
Node add\[maxn\];

int main() {
    scanf("%d%d%d", &st, &N, &K);
    for(int i = 0; i < N; i ++) {
        scanf("%d%d%d", &n.address, &n.val, &n.nx);
        add\[n.address\] = n;
    }

    int first = st;
    while(first != -1) {
        l.push_back(add\[first\]);
        first = add\[first\].nx;
    }

    int sz = l.size();
    for(int i = 0; i < sz; i ++) {
        if(l\[i\].val < 0)
            ans.push_back(l\[i\]);
    }
    for(int i = 0; i < sz; i ++) {
        if(l\[i\].val >= 0 && l\[i\].val <= K)
            ans.push_back(l\[i\]);
    }
    for(int i = 0; i < sz; i ++) {
        if(l\[i\].val > K)
            ans.push_back(l\[i\]);
    }

    for(int i = 0; i < sz; i ++) {
        ans\[i\].nx = ans\[i + 1\].address;
        if(i != sz - 1)
            printf("%05d %d %05d\\n", ans\[i\].address, ans\[i\].val, ans\[i\].nx);
        else
            printf("%05d %d -1\\n", ans\[i\].address, ans\[i\].val);
    }
    return 0;
}
```