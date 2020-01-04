---
title: Pat_1056（乙级）
url: 1735.html
id: 1735
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:42:30
tags:
  - pat
---

1056 组合数的和 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805271455449088)

给定 N 个非 0 的个位数字，用其中任意 2 个数字都可以组合成 1 个 2 位的数字。要求所有可能组合出来的 2 位数字的和。例如给定 2、5、8，则可以组合出：25、28、52、58、82、85，它们的和为330。

### 输入格式：

输入在一行中先给出 N（1 < N < 10），随后给出 N 个不同的非 0 个位数字。数字间以空格分隔。

### 输出格式：

输出所有可能组合出来的2位数字的和。

### 输入样例：

    3 2 8 5
    

### 输出样例：

    330

代码：
```
#include<iostream>
#include<string.h>
#include<math.h>
#include<algorithm>
#include<vector>
//思路对三个数进行全排列，然后只取前两位即可
using namespace std;

int sum = 0;
vector<int> dir;

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

void Permutation(string str,int index){
    if(str == ""){
        return ;
    }
    if(index == str.length() - 1){
        int temp = strToNum(str.substr(0,2));
        //去重复 如果为 输入为 3个1  通过全排列得到的结果为 111  111 111 111 111 111 111 然后进行去重 最后只得到了 11
        if(find(dir.begin(),dir.end(),temp) == dir.end()){
            sum += temp;
            dir.push_back(temp);
        }
        return ;
    }
    for(int i=index;i<str.length();i++){
        //首部和他后面的字符进行交换
        char temp = str\[i\];
        str\[i\] = str\[index\];
        str\[index\] = temp;
        //递归求后面的字符的排列
        Permutation(str,index+1);
        //由于前面交换了一下还要交换回来
        temp = str\[i\];
        str\[i\] = str\[index\];
        str\[index\] = temp;
    }
}


int main(){
    int num;
    cin>>num;
    char ch\[num\];
    string s1 = "";
    for(int i=0;i<num;i++){
        cin>>ch\[i\];
        s1 += ch\[i\];
    }
    Permutation(s1,0);
    cout<<sum<<endl;
    return 0;
}
```