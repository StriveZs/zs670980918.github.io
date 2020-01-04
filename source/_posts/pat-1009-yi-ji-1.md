---
title: Pat_1009（乙级）
url: 1637.html
id: 1637
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:59:16
tags:
  - pat
---

1009 说反话 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805314941992960

给定一句英语，要求你编写程序，将句中所有单词的顺序颠倒输出。

### 输入格式：

测试输入包含一个测试用例，在一行内给出总长度不超过 80 的字符串。字符串由若干单词和若干空格组成，其中单词是由英文字母（大小写有区分）组成的字符串，单词之间用 1 个空格分开，输入保证句子末尾没有多余的空格。

### 输出格式：

每个测试用例的输出占一行，输出倒序后的句子。

### 输入样例：

    Hello World Here I Come
    

### 输出样例：

    Come I Here World Hello

代码：
```
#include<iostream>
#include<deque>
#include<string.h>

using namespace std;

int main(){
    deque<string> Queue;
    deque<string>::iterator pos;
    string s1;
    int sum = 0;
    while(cin>>s1){
        Queue.push_front(s1);
        sum++;
        if(cin.get()=='\\n'){
            break;
        }
    }
    for(pos = Queue.begin();pos!=Queue.end()-1;pos++)
        cout<<*pos<<" ";
    pos = Queue.end()-1;
    cout<<*pos<<endl;
    return 0;
}
```