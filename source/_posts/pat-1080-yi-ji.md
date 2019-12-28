---
title: Pat_1080（乙级）
url: 1784.html
id: 1784
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:18:39
tags:
---

1080 MOOC期终成绩 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805261493977088)

对于在中国大学MOOC（[http://www.icourse163.org/](http://www.icourse163.org/) ）学习“数据结构”课程的学生，想要获得一张合格证书，必须首先获得不少于200分的在线编程作业分，然后总评获得不少于60分（满分100）。总评成绩的计算公式为 G=(G​mid−term​​×40%+G​final​​×60%)，如果 G​mid−term​​>G​final​​；否则总评 G 就是 G​final​​。这里 G​mid−term​​ 和 G​final​​ 分别为学生的期中和期末成绩。 现在的问题是，每次考试都产生一张独立的成绩单。本题就请你编写程序，把不同的成绩单合为一张。

### 输入格式：

输入在第一行给出3个整数，分别是 P（做了在线编程作业的学生数）、M（参加了期中考试的学生数）、N（参加了期末考试的学生数）。每个数都不超过10000。 接下来有三块输入。第一块包含 P 个在线编程成绩 G​p​​；第二块包含 M 个期中考试成绩 G​mid−term​​；第三块包含 N 个期末考试成绩 G​final​​。每个成绩占一行，格式为：`学生学号 分数`。其中`学生学号`为不超过20个字符的英文字母和数字；`分数`是非负整数（编程总分最高为900分，期中和期末的最高分为100分）。

### 输出格式：

打印出获得合格证书的学生名单。每个学生占一行，格式为： `学生学号` G​p​​ G​mid−term​​ G​final​​ G 如果有的成绩不存在（例如某人没参加期中考试），则在相应的位置输出“−1”。输出顺序为按照总评分数（四舍五入精确到整数）递减。若有并列，则按学号递增。题目保证学号没有重复，且至少存在1个合格的学生。

### 输入样例：

    6 6 7
    01234 880
    a1903 199
    ydjh2 200
    wehu8 300
    dx86w 220
    missing 400
    ydhfu77 99
    wehu8 55
    ydjh2 98
    dx86w 88
    a1903 86
    01234 39
    ydhfu77 88
    a1903 66
    01234 58
    wehu8 84
    ydjh2 82
    missing 99
    dx86w 81
    

### 输出样例：

    missing 400 -1 99 99
    ydjh2 200 98 82 88
    dx86w 220 88 81 84
    wehu8 300 55 84 84

代码：

#include<iostream>
#include<map>
#include<algorithm>
#include<string.h>
#include<vector>
#include<math.h>

using namespace std;

struct Student{
    int P;
    int Gm;
    int Gf;
    int G;
    Student();
};
//结构体设置初值
Student::Student(){
    P = -1;
    Gm = -1;
    Gf = -1;
    G = -1;
}

struct Node{
    string name;
    int P1;
    int Gm1;
    int Gf1;
    int G1;
};

bool cmp(Node t1,Node t2){
    if(t1.G1 == t2.G1){
        return t1.name < t2.name;
    }
    else{
        return t1.G1 > t2.G1;
    }
}

int main(){
    map<string,Student> studentList;
    map<string,Student>::iterator pos;
    vector<Node> list1;
    vector<Node>::iterator pos1;
    int P,M,N;
    cin>>P>>M>>N;
    for(int i=0;i<P;i++){
        string temp;
        int grade;
        cin>>temp>>grade;
        studentList\[temp\].P = grade;
    }
    for(int i=0;i<M;i++){
        string temp;
        int grade;
        cin>>temp>>grade;
        studentList\[temp\].Gm = grade;
    }
    for(int i=0;i<N;i++){
        string temp;
        int grade;
        cin>>temp>>grade;
        studentList\[temp\].Gf = grade;
    }
    for(pos = studentList.begin();pos!=studentList.end();pos++){
        if(pos->second.Gm > pos->second.Gf){
            pos->second.G = round((float)(pos->second.Gm * 0.4 + pos->second.Gf * 0.6));
        }
        else{
            pos->second.G = pos->second.Gf;
        }
        if(pos->second.P >= 200 && pos->second.G >= 60){
            Node nodes = {pos->first,pos->second.P,pos->second.Gm,pos->second.Gf,pos->second.G};
            list1.push_back(nodes);
        }
        //cout<<pos->first<<" "<<pos->second.P<<" "<<pos->second.Gm<<" "<<pos->second.Gf<<" "<<pos->second.G<<endl;
    }
    sort(list1.begin(),list1.end(),cmp);
    for(pos1 = list1.begin();pos1!= list1.end();pos1++){
        cout<<(\*pos1).name<<" "<<(\*pos1).P1<<" "<<(\*pos1).Gm1<<" "<<(\*pos1).Gf1<<" "<<(*pos1).G1<<endl;
    }
    return 0;
}