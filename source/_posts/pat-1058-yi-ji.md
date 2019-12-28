---
title: Pat_1058（乙级）
url: 1739.html
id: 1739
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:44:20
tags:
---

1058 选择题 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805270356541440)

批改多选题是比较麻烦的事情，本题就请你写个程序帮助老师批改多选题，并且指出哪道题错的人最多。

### 输入格式：

输入在第一行给出两个正整数 N（≤ 1000）和 M（≤ 100），分别是学生人数和多选题的个数。随后 M 行，每行顺次给出一道题的满分值（不超过 5 的正整数）、选项个数（不少于 2 且不超过 5 的正整数）、正确选项个数（不超过选项个数的正整数）、所有正确选项。注意每题的选项从小写英文字母 a 开始顺次排列。各项间以 1 个空格分隔。最后 N 行，每行给出一个学生的答题情况，其每题答案格式为 `(选中的选项个数 选项1 ……)`，按题目顺序给出。注意：题目保证学生的答题情况是合法的，即不存在选中的选项数超过实际选项数的情况。

### 输出格式：

按照输入的顺序给出每个学生的得分，每个分数占一行。注意判题时只有选择全部正确才能得到该题的分数。最后一行输出错得最多的题目的错误次数和编号（题目按照输入的顺序从 1 开始编号）。如果有并列，则按编号递增顺序输出。数字间用空格分隔，行首尾不得有多余空格。如果所有题目都没有人错，则在最后一行输出 `Too simple`。

### 输入样例：

    3 4 
    3 4 2 a c
    2 5 1 b
    5 3 2 b c
    1 5 4 a b d e
    (2 a c) (2 b d) (2 a c) (3 a b e)
    (2 a c) (1 b) (2 a b) (4 a b d e)
    (2 b d) (1 e) (2 b c) (4 a b c d)
    

### 输出样例：

    3
    6
    5
    2 2 3 4

代码：

#include<iostream>
#include<cstdio>
#include<string.h>
#include<algorithm>
using namespace std;

struct Answer{
    int fenzhi; //分值
    int num_xuan; //选项个数
    int num_yes; //正确选项个数
    string ans; //答案
};

struct Statistics{
    int num_error; //出错数
    int number; //编号
};

bool cmp(Statistics a,Statistics b){
    if(a.num\_error == b.num\_error){
        return a.number < b.number;
    }
    else{
       return a.num\_error > b.num\_error;
    }
}

int main(){
    int N,M,sum=0;//sum总分
    cin>>N>>M;
    Answer ans_list\[M\];
    for(int i=0;i<M;i++){
        int t1,t2,t3;
        cin>>t1>>t2>>t3;
        sum += t1;
        ans_list\[i\].fenzhi = t1;
        ans\_list\[i\].num\_xuan = t2;
        ans\_list\[i\].num\_yes = t3;
        string s1="";
        for(int j=0;j<t3;j++){
            char t;
            cin>>t;
            s1 += t;
        }
        ans_list\[i\].ans = s1;
    }
    Statistics dir\[M\] = {0,0}; //出错统计
    int grade\[N\] = {0}; //学生得分
    getchar();//去掉回车
    for(int i=0;i<N;i++){
        string s1;
        getline(cin,s1);
        int j=0; //题号
        int index = 0; //下标
        string temp = "";
        int t = 0;
        while(index < s1.length()){
            if(s1\[index\] == '('){
                index++;
                if(s1\[index\]>='0' && s1\[index\]<='9'){
                    t = s1\[index\] - '0';
                    index++;
                }
                continue;
            }
            else if(s1\[index\] >= 'a' && s1\[index\] <= 'z'){
                temp += s1\[index\];
                index++;
                //cout<<j<<endl;
                //cout<<temp<<endl;
                continue;
            }
            else if(s1\[index\] == ')'){
                if(t != ans\_list\[j\].num\_yes){
                    dir\[j\].number = j;
                    dir\[j\].num_error++;
                }
                else{
                    if(temp == ans_list\[j\].ans){
                        grade\[i\] += ans_list\[j\].fenzhi;
                    }
                    else{
                        dir\[j\].number = j;
                        dir\[j\].num_error++;
                    }
                }
                j++;
                temp = "";
                index++;
                t = 0;
                continue;
            }
            else{
                index++;
            }
        }
    }
    //输出每个学生的得分
    for(int i=0;i<N;i++){
        cout<<grade\[i\]<<endl;
    }
    sort(dir,dir+M,cmp);
    /*for(int i=0;i<M;i++){
        cout<<dir\[i\].number<<" "<<dir\[i\].num_error<<endl;
    }*/
    if(dir\[0\].num_error == 0){
        cout<<"Too simple"<<endl;
    }
    else{
        int j=0;
        bool flag = true;
        //寻找相同的出错书
        while(flag){
            if(dir\[j\].num\_error != dir\[j+1\].num\_error){
                flag = false;
            }
            else{
                j++;
            }
        }
        //打印结果
        cout<<dir\[0\].num_error<<" ";
        for(int i=0;i<=j;i++){
            if(i != j){
                cout<<dir\[i\].number + 1<<" ";
            }
            else{
                cout<<dir\[i\].number + 1;
            }
        }
        cout<<endl;
    }
    return 0;
}