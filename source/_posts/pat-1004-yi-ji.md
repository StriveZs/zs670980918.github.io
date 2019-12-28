---
title: Pat_1004（乙级）
url: 1627.html
id: 1627
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:53:15
tags:
---

1004 成绩排名 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805321640296448

读入 n（>0）名学生的姓名、学号、成绩，分别输出成绩最高和成绩最低学生的姓名和学号。

### 输入格式：

每个测试输入包含 1 个测试用例，格式为

    第 1 行：正整数 n
    第 2 行：第 1 个学生的姓名 学号 成绩
    第 3 行：第 2 个学生的姓名 学号 成绩
      ... ... ...
    第 n+1 行：第 n 个学生的姓名 学号 成绩
    

其中`姓名`和`学号`均为不超过 10 个字符的字符串，成绩为 0 到 100 之间的一个整数，这里保证在一组测试用例中没有两个学生的成绩是相同的。

### 输出格式：

对每个测试用例输出 2 行，第 1 行是成绩最高学生的姓名和学号，第 2 行是成绩最低学生的姓名和学号，字符串间有 1 空格。

### 输入样例：

    3
    Joe Math990112 89
    Mike CS991301 100
    Mary EE990830 95
    

### 输出样例：

    Mike CS991301
    Joe Math990112

代码：

#include<iostream>
#include<string>
#include<deque>

using namespace std;

struct paixu{
    string name;
    string ID;
    int grade;
};

void zijian(int n\[\],int len){
    int t = len;
    bool flag = false;
    do{
        if((n\[t\]-1)>=0){
            n\[t\]--;
            flag = true;
        }
        else{
            n\[t\] = 9;
            t--;
        }
    }while(flag!=true);
}

bool equalZero(int n\[\],int len){
    bool flag = true;
    for(int i=0;i<len;i++){
        if(n\[i\]!=0){
            flag = false;
            break;
        }
    }
    return flag;
}
//选择排序
void Sorted(deque<paixu> test){
    int t;
    for(int i=0;i<test.size()-1;i++){
       t = i;
       for(int j=i+1;j<test.size();j++){
            if(test\[j\].grade > test\[t\].grade){
                swap(test\[i\],test\[j\]);
            }
       }
    }
}

int main(){
    deque<paixu> mess;
    deque<paixu> result;
    string number;
    cin>>number;
    int BigNum\[number.length()\];
    for(int i=number.length()-1;i>=0;i--){
        BigNum\[i\] = number\[i\] - '0';
    }
    while(equalZero(BigNum,number.length()) == false){
        paixu text;
        string s1;
        string s2;
        int num;
        cin>>s1;
        cin>>s2;
        cin>>num;
        text.name = s1;
        text.ID = s2;
        text.grade = num;
        mess.push_back(text);
        zijian(BigNum,number.length()-1);
    }
    int t;
    for(int i=0;i<mess.size()-1;i++){
       t =  i;
       for(int j=i+1;j<mess.size();j++){
            if(mess\[j\].grade > mess\[t\].grade){
                swap(mess\[t\],mess\[j\]);
            }
       }
    }
    /*for(int i=0;i<mess.size();i++){
        cout<<mess\[i\].grade<<endl;
    }*/
    cout<<mess\[0\].name<<" "<<mess\[0\].ID<<endl;
    cout<<mess\[mess.size()-1\].name<<" "<<mess\[mess.size()-1\].ID<<endl;
    return 0;
}