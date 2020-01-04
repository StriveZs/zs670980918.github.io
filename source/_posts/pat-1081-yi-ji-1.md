---
title: Pat_1081（乙级）
url: 1786.html
id: 1786
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:20:58
tags:
  - pat
---

1081 检查密码 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805261217153024)

本题要求你帮助某网站的用户注册模块写一个密码合法性检查的小功能。该网站要求用户设置的密码必须由不少于6个字符组成，并且只能有英文字母、数字和小数点 `.`，还必须既有字母也有数字。

### 输入格式：

输入第一行给出一个正整数 N（≤ 100），随后 N 行，每行给出一个用户设置的密码，为不超过 80 个字符的非空字符串，以回车结束。

### 输出格式：

对每个用户的密码，在一行中输出系统反馈信息，分以下5种：

*   如果密码合法，输出`Your password is wan mei.`；
*   如果密码太短，不论合法与否，都输出`Your password is tai duan le.`；
*   如果密码长度合法，但存在不合法字符，则输出`Your password is tai luan le.`；
*   如果密码长度合法，但只有字母没有数字，则输出`Your password needs shu zi.`；
*   如果密码长度合法，但只有数字没有字母，则输出`Your password needs zi mu.`。

### 输入样例：

    5
    123s
    zheshi.wodepw
    1234.5678
    WanMei23333
    pass*word.6
    

### 输出样例：

    Your password is tai duan le.
    Your password needs shu zi.
    Your password needs zi mu.
    Your password is wan mei.
    Your password is tai luan le.

代码（不通过的版本）：
```
#include<iostream>
#include<string.h>
#include<algorithm>
//废弃版本 花费太多时间了 时间复杂度不符合要求
using namespace std;
//判断是否含有非法字符
bool IsIllegal(string s1){
    bool flag = true;
    for(int i=0;i<s1.length();i++){
        if((s1\[i\] >= '0' && s1\[i\] <= '9') || (s1\[i\] >= 'A' && s1\[i\] <= 'Z') || (s1\[i\] >= 'a' && s1\[i\] <= 'z') || (s1\[i\] == '.')){
            continue;
        }
        else{
            flag = false;
            break;
        }
    }
    return flag;
}

//判断是否含有数字
bool IsHaveNumber(string s1){
    bool flag = true;
    for(int i=0;i<=9;i++){
        char t = (i+'0');
        if(find(s1.begin(),s1.end(),s1.begin(),t)==string::npos){
            flag = false;
            break;
        }
    }
    return flag;
}

int main(){
    int num = 0;
    cin>>num;
    for(int i=0;i<num;i++){
        string s1;
        cin>>s1;
        bool flag = true;
        if(s1.length() < 6){
            cout<<"Your password is tai duan le."<<endl;
            continue;
        }
        else if(!IsIllegal(s1)){
            cout<<"Your password is tai duan le."<<endl;
            continue;
        }
        else if(IsHaveNumber(s1){
            cout<<"Your password needs zi mu."<<endl;
            continue;
        }
    }
    return 0;
}
```
修改后的版本：
```
#include <iostream>
#include <cctype>
using namespace std;
int main() {
    int n;
    cin >> n; getchar();
    for (int i = 0; i < n; i++) {
        string s;
        getline(cin, s);
        if (s.length() >= 6) {
            int invalid = 0, hasAlpha = 0, hasNum = 0;
            for (int j = 0; j < s.length(); j++) {
                if (s\[j\] != '.' && !isalnum(s\[j\])) invalid = 1;
                else if (isalpha(s\[j\])) hasAlpha = 1;
                else if (isdigit(s\[j\])) hasNum = 1;
            }
            if (invalid == 1) cout << "Your password is tai luan le.\\n";
            else if (hasNum == 0) cout << "Your password needs shu zi.\\n";
            else if (hasAlpha == 0) cout << "Your password needs zi mu.\\n";
            else cout << "Your password is wan mei.\\n";
        } else
            cout << "Your password is tai duan le.\\n";
    }
    return 0;
}
```