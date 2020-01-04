---
title: Pat_1082（乙级）
url: 1788.html
id: 1788
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:21:52
tags:
  - pat
---

1082 射击比赛 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805260990660608)

本题目给出的射击比赛的规则非常简单，谁打的弹洞距离靶心最近，谁就是冠军；谁差得最远，谁就是菜鸟。本题给出一系列弹洞的平面坐标(x,y)，请你编写程序找出冠军和菜鸟。我们假设靶心在原点(0,0)。

### 输入格式：

输入在第一行中给出一个正整数 N（≤ 10 000）。随后 N 行，每行按下列格式给出：

    ID x y
    

其中 `ID` 是运动员的编号（由 4 位数字组成）；`x` 和 `y` 是其打出的弹洞的平面坐标(`x`,`y`)，均为整数，且 0 ≤ |`x`|, |`y`| ≤ 100。题目保证每个运动员的编号不重复，且每人只打 1 枪。

### 输出格式：

输出冠军和菜鸟的编号，中间空 1 格。题目保证他们是唯一的。

### 输入样例：

    3
    0001 5 7
    1020 -1 3
    0233 0 -1
    

### 输出样例：

    0233 0001

代码：
```
#include<iostream>
#include<math.h>
#include<algorithm>

using namespace std;

struct Player{
    string name;
    float distance;
};

bool cmp(Player a,Player b){
    return a.distance > b.distance;
}

int main(){
    int num;
    cin>>num;
    Player players\[num\];
    for(int i=0;i<num;i++){
        string s1;
        cin>>s1;
        float t1,t2;
        cin>>t1>>t2;
        float ds = sqrt(t1\*t1 + t2\*t2);
        players\[i\].name = s1;
        players\[i\].distance = ds;
    }
    sort(players,players+num,cmp);
    cout<<players\[num-1\].name<<" "<<players\[0\].name<<endl;
    return 0;
}
```