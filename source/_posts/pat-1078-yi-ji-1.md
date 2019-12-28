---
title: Pat_1078（乙级）
url: 1780.html
id: 1780
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:16:17
tags:
---

1078 字符串压缩与解压 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805262018265088)

文本压缩有很多种方法，这里我们只考虑最简单的一种：把由相同字符组成的一个连续的片段用这个字符和片段中含有这个字符的个数来表示。例如 `ccccc` 就用 `5c` 来表示。如果字符没有重复，就原样输出。例如 `aba` 压缩后仍然是 `aba`。 解压方法就是反过来，把形如 `5c` 这样的表示恢复为 `ccccc`。 本题需要你根据压缩或解压的要求，对给定字符串进行处理。这里我们简单地假设原始字符串是完全由英文字母和空格组成的非空字符串。

### 输入格式：

输入第一行给出一个字符，如果是 `C` 就表示下面的字符串需要被压缩；如果是 `D` 就表示下面的字符串需要被解压。第二行给出需要被压缩或解压的不超过 1000 个字符的字符串，以回车结尾。题目保证字符重复个数在整型范围内，且输出文件不超过 1MB。

### 输出格式：

根据要求压缩或解压字符串，并在一行中输出结果。

### 输入样例 1：

    C
    TTTTThhiiiis isssss a   tesssst CAaaa as
    

### 输出样例 1：

    5T2h4is i5s a3 te4st CA3a as
    

### 输入样例 2：

    D
    5T2h4is i5s a3 te4st CA3a as10Z
    

### 输出样例 2：

    TTTTThhiiiis isssss a   tesssst CAaaa asZZZZZZZZZZ

代码：

#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>

using namespace std;

int strToNum(string s1){
    int len = s1.length();
    int num = 0;
    reverse(s1.begin(),s1.end());
    while(len > 0){
        num += (s1\[len-1\] - '0')*round(pow(10,len-1));
        len--;
    }
    return num;
}

int main(){
    char tt;
    cin>>tt;
    string s1="";
    cin.get();
    if(tt == 'C'){
        getline(cin,s1);
        int index = 0,num = 1;
        char temp = s1\[index++\];
        while(index <= s1.length()){
            if(temp == s1\[index\]){
                num++;
                index++;
                continue;
            }
            else if(temp != s1\[index\]){
                if(num == 1){
                    cout<<temp;
                }
                else{
                    cout<<num<<temp;
                }
                temp = s1\[index++\];
                num = 1;
            }
        }
        cout<<endl;
    }
    else if(tt == 'D'){
        getline(cin,s1);
        int index = 0,num = 0;
        char temp;
        while(index < s1.length()){
            if(s1\[index\] >= '0' && s1\[index\] <= '9'){
                string t = "";
                t += s1\[index++\];
                while(s1\[index\] >= '0' && s1\[index\] <= '9'){
                    t += s1\[index++\];
                }
                num = strToNum(t);
                temp =  s1\[index++\];
                string s2(num,temp);
                cout<<s2;
            }
            else{
                cout<<s1\[index++\];
            }
        }
        cout<<endl;
    }
    return 0;
}