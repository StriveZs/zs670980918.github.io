---
title: Pat_1095（乙级）
url: 1814.html
id: 1814
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:36:54
tags:
---

1095 解码PAT准考证 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1071786104348536832)

PAT 准考证号由 4 部分组成：

*   第 1 位是级别，即 `T` 代表顶级；`A` 代表甲级；`B` 代表乙级；
*   第 2~4 位是考场编号，范围从 101 到 999；
*   第 5~10 位是考试日期，格式为年、月、日顺次各占 2 位；
*   最后 11~13 位是考生编号，范围从 000 到 999。

现给定一系列考生的准考证号和他们的成绩，请你按照要求输出各种统计信息。

### 输入格式：

输入首先在一行中给出两个正整数 N（≤10​4​​）和 M（≤100），分别为考生人数和统计要求的个数。 接下来 N 行，每行给出一个考生的准考证号和其分数（在区间 \[0,100\] 内的整数），其间以空格分隔。 考生信息之后，再给出 M 行，每行给出一个统计要求，格式为：`类型 指令`，其中

*   `类型` 为 1 表示要求按分数非升序输出某个指定级别的考生的成绩，对应的 `指令` 则给出代表指定级别的字母；
*   `类型` 为 2 表示要求将某指定考场的考生人数和总分统计输出，对应的 `指令` 则给出指定考场的编号；
*   `类型` 为 3 表示要求将某指定日期的考生人数分考场统计输出，对应的 `指令` 则给出指定日期，格式与准考证上日期相同。

### 输出格式：

对每项统计要求，首先在一行中输出 `Case #: 要求`，其中 `#` 是该项要求的编号，从 1 开始；`要求` 即复制输入给出的要求。随后输出相应的统计结果：

*   `类型` 为 1 的指令，输出格式与输入的考生信息格式相同，即 `准考证号 成绩`。对于分数并列的考生，按其准考证号的字典序递增输出（题目保证无重复准考证号）；
*   `类型` 为 2 的指令，按 `人数 总分` 的格式输出；
*   `类型` 为 3 的指令，输出按人数非递增顺序，格式为 `考场编号 总人数`。若人数并列则按考场编号递增顺序输出。

如果查询结果为空，则输出 `NA`。

### 输入样例：

    8 4
    B123180908127 99
    B102180908003 86
    A112180318002 98
    T107150310127 62
    A107180908108 100
    T123180908010 78
    B112160918035 88
    A107180908021 98
    1 A
    2 107
    3 180908
    2 999
    

### 输出样例：

    Case 1: 1 A
    A107180908108 100
    A107180908021 98
    A112180318002 98
    Case 2: 2 107
    3 260
    Case 3: 3 180908
    107 2
    123 2
    102 1
    Case 4: 2 999
    NA

代码：

#include <iostream>
#include <cstring>
#include <algorithm>
#include <map>
#include <vector>
using namespace std;
struct student{
    string id;
    int score;
};
struct examcase2{
    int allscore=0;
    int people=0;
};
struct examroom{
    string room;
    int people=0;
};
bool cmp(student a,student b)
{
    if(a.score!=b.score) return a.score>b.score;
    else return a.id<b.id;
}
bool cmp1(examroom a,examroom b)
{
    if(a.people!=b.people) return a.people>b.people;
    else return a.room<b.room;
}
int main()
{
    int N,M;
    scanf("%d %d",&N,&M);            //用cin.cout会超时
    map<string,vector<student>>  case1;     //按等级分；
    map<string,examcase2> case2;             //按教室分；
    map<string,map<string,examroom>>  case3;     //按日期分；
    for(int i=0;i<N;i++)
    {
        student s;
        char id\[14\];
        scanf("%s %d",id,&s.score);
        s.id=id;
        string ranks=s.id.substr(0,1);
        string exroom=s.id.substr(1,3);
        string date=s.id.substr(4,6);
        case1\[ranks\].push_back(s);        //将s放入同一个等级的动态数组中
        case2\[exroom\].allscore+=s.score;    //该考场的总成绩增加
        case2\[exroom\].people++;            //该考场的总人数增加
        case3\[date\]\[exroom\].room=exroom;    //这个日期考试的这个考场的考场号
        case3\[date\]\[exroom\].people++;        //这个日期考试的这个考场的人数
    }
    for(int i=1;i<=M;i++)
    {
        int classi;
        char request\[7\];
        memset(request,0,sizeof(request));
        scanf("%d %s",&classi,request);
        printf("Case %d: %d %s\\n",i,classi,request);
        int flag=1;
        switch(classi)
        {
            case 1:
                {
                    vector<student>  ttt=case1\[request\];    //取出指定级别的集合
                    sort(ttt.begin(),ttt.end(),cmp);        //排序
                    for(auto it=ttt.begin();it!=ttt.end();it++)
                    {
                        printf("%s %d\\n",(\*it).id.c_str(),(\*it).score);//输出
                        flag=0;                    //产生了输出，该要求有结果
                    }
                    break;
                }
            case 2:
                {
                    examcase2 ttt=case2\[request\];        //取出指定考场的信息
                    if(ttt.people!=0)                //该考场有人考试
                    {
                        printf("%d %d\\n",ttt.people,ttt.allscore);    //输出结果
                        flag=0;
                    }
                    break;
                }
            case 3:
                {
                    map<string,examroom> ttt=case3\[request\]; //取出该天考试的所有考场的信息
                    int i=0,len=ttt.size();        //len--该天有len个考场进行考试
                    examroom e\[len\];
                    for(auto it=ttt.begin();it!=ttt.end();it++)
                    {
                        e\[i++\]=it->second;        //将考场信息存入数组
                    }
                    sort(e,e+len,cmp1);    //进行排序
                    for(i=0;i<len;i++)
                    {
                        printf("%s %d\\n",e\[i\].room.c_str(),e\[i\].people);//输出结果
                        flag=0;
                    }
                    break;
                }
        }
        if(flag)  printf("NA\\n");    //没有符合条件的结果，则输出NA
    }
    return 0;
}