---
title: Pat_1052（乙级）
url: 1727.html
id: 1727
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:32:20
tags:
  - pat
---

1052 卖个萌 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805273883951104)

萌萌哒表情符号通常由“手”、“眼”、“口”三个主要部分组成。简单起见，我们假设一个表情符号是按下列格式输出的：

    [左手]([左眼][口][右眼])[右手]
    

现给出可选用的符号集合，请你按用户的要求输出表情。

### 输入格式：

输入首先在前三行顺序对应给出手、眼、口的可选符号集。每个符号括在一对方括号 `[]`内。题目保证每个集合都至少有一个符号，并不超过 10 个符号；每个符号包含 1 到 4 个非空字符。 之后一行给出一个正整数 K，为用户请求的个数。随后 K 行，每行给出一个用户的符号选择，顺序为左手、左眼、口、右眼、右手——这里只给出符号在相应集合中的序号（从 1 开始），数字间以空格分隔。

### 输出格式：

对每个用户请求，在一行中输出生成的表情。若用户选择的序号不存在，则输出 `Are you kidding me? @\/@`。

### 输入样例：

    [╮][╭][o][~\][/~]  [<][>]
     [╯][╰][^][-][=][>][<][@][⊙]
    [Д][▽][_][ε][^]  ...
    4
    1 1 2 2 2
    6 8 1 5 5
    3 3 4 3 3
    2 10 3 9 3
    

### 输出样例：

    ╮(╯▽╰)╭
    <(@Д=)/~
    o(^ε^)o
    Are you kidding me? @\/@

代码（有一个测试点没通过）：
```
#include<iostream>
#include<cstdio>
#include<vector>

using namespace std;

int main(){
    vector<vector<string> > str;
    for(int i=0;i<3;i++){
        vector<string> list1;
        string temp;
        getline(cin,temp);
        for(int j=0;j<temp.length();j++){
            if(temp\[j\] == '\['){
                int k = j+1;
                while(k++ < temp.length()){
                    if(temp\[k\] == '\]'){
                        list1.push_back(temp.substr(j+1,k-j-1));
                        break;
                    }
                }
            }
        }
        str.push_back(list1);
    }
    /*for(int i=0;i<3;i++){
        for(int j=0;j<str\[i\].size();j++){
            cout<<str\[i\]\[j\]<<" ";
        }
        cout<<endl;
    }*/
    int num;
    cin>>num;
    for(int i=0;i<num;i++){
        int a,b,c,d,e;
        cin>>a>>b>>c>>d>>e;
        if(a > str\[0\].size()|| b > str\[1\].size() || c > str\[2\].size() || d > str\[1\].size() || e > str\[0\].size()){
            cout<<"Are you kidding me? @\\\/@"<<endl;
        }
        else{
            cout<<str\[0\]\[a-1\]<<"("<<str\[1\]\[b-1\]<<str\[2\]\[c-1\]<<str\[1\]\[d-1\]<<")"<<str\[0\]\[e-1\]<<endl;
        }
    }

    return 0;
}

修改版本：

#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector<vector<string> > v;
    for(int i = 0; i < 3; i++) {
        string s;
        getline(cin, s);
        vector<string> row;
        int j = 0, k = 0;
        while(j < s.length()) {
            if(s\[j\] == '\[') {
                while(k++ < s.length()) {
                    if(s\[k\] == '\]') {
                        row.push_back(s.substr(j+1, k-j-1));
                        break;
                    }
                }
            }
            j++;
        }
        v.push_back(row);
    }
    int n;
    cin >> n;
    for(int i = 0; i < n; i++) {
        int a, b, c, d, e;
        cin >> a >> b >> c >> d >> e;
        if(a > v\[0\].size() || b > v\[1\].size() || c > v\[2\].size() || d > v\[1\].size() || e > v\[0\].size() || a < 1 || b < 1 || c < 1 || d < 1 || e < 1) {
            cout << "Are you kidding me? @\\\/@" << endl;
            continue;
        }
        cout << v\[0\]\[a-1\] << "(" << v\[1\]\[b-1\] << v\[2\]\[c-1\] << v\[1\]\[d-1\] << ")" << v\[0\]\[e-1\] << endl;
    }
    return 0;
}
```