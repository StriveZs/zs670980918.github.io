---
title: Pat_1083（乙级）
url: 1790.html
id: 1790
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:22:57
tags:
---

1083 是否存在相等的差 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805260780945408)

给定 N 张卡片，正面分别写上 1、2、……、N，然后全部翻面，洗牌，在背面分别写上 1、2、……、N。将每张牌的正反两面数字相减（大减小），得到 N 个非负差值，其中是否存在相等的差？

### 输入格式：

输入第一行给出一个正整数 N（2 ≤ N ≤ 10 000），随后一行给出 1 到 N 的一个洗牌后的排列，第 i 个数表示正面写了 i 的那张卡片背面的数字。

### 输出格式：

按照“差值 重复次数”的格式从大到小输出重复的差值及其重复的次数，每行输出一个结果。

### 输入样例：

    8
    3 5 8 6 2 1 4 7
    

### 输出样例：

    5 2
    3 3
    2 2

代码：

#include<iostream>
#include<map>
#include<vector>
#include<algorithm>

using namespace std;

struct Node{
    int t1;
    int t2;
};

bool cmp(Node a,Node b){
    return a.t1 > b.t1;
}

int main(){
    map<int,int> dir;
    map<int,int>::iterator pos;
    vector<Node> dir_vec;
    vector<Node>::iterator pos1;
    int num;
    cin>>num;
    for(int i=0;i<num;i++){
        int cha,temp;
        cin>>temp;
        if(temp > i+1){
            cha = temp - (i+1);
        }
        else{
            cha = (i+1) - temp;
        }
        if(dir.count(cha) == 0){
            dir\[cha\] = 1;
        }
        else{
            dir\[cha\] += 1;
        }
    }
    for(pos=dir.begin();pos!=dir.end();pos++){
        Node node = {(\*pos).first,(\*pos).second};
        if((*pos).second > 1){
            dir\_vec.push\_back(node);
        }
    }
    if(dir_vec.empty()){
        cout<<endl;
    }
    else{
       sort(dir\_vec.begin(),dir\_vec.end(),cmp);
        for(pos1 = dir\_vec.begin();pos1!=dir\_vec.end();pos1++){
            cout<<(\*pos1).t1<<" "<<(\*pos1).t2<<endl;
        }
    }
    return 0;
}