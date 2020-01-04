---
title: Pat_1042（乙级）
url: 1706.html
id: 1706
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:17:10
tags:
  - pat
---

1042 字符统计 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805280817135616)

请编写程序，找出一段给定文字中出现最频繁的那个英文字母。

### 输入格式：

输入在一行中给出一个长度不超过 1000 的字符串。字符串由 ASCII 码表中任意可见字符及空格组成，至少包含 1 个英文字母，以回车结束（回车不算在内）。

### 输出格式：

在一行中输出出现频率最高的那个英文字母及其出现次数，其间以空格分隔。如果有并列，则输出按字母序最小的那个字母。统计时不区分大小写，输出小写字母。

### 输入样例：

    This is a simple TEST.  There ARE numbers and other symbols 1&2&3...........
    

### 输出样例：

    e 7

代码：
```
#include<iostream>
#include<string.h>
#include<map>
#include<vector>
#include<algorithm>

using namespace std;

typedef pair<char, int> PAIR;

ostream& operator<<(ostream& out, const PAIR& p) {
  return out << p.first << " " << p.second;
}

bool cmp\_by\_value(const PAIR& t1,const PAIR& t2){
    if(t1.second == t2.second){
        return t1.first < t2.first;
    }
    else{
        return t1.second > t2.second;
    }

}

int main(){
    map<char,int> dir;
    string s1;
    getline(cin,s1);
    transform(s1.begin(),s1.end(),s1.begin(),::tolower);
    //cout<<s1<<endl;
    for(int i=0;i<s1.length();i++){
        if(s1\[i\]>='a' && s1\[i\]<='z'){
            if(dir.count(s1\[i\]) == 0){
                dir\[s1\[i\]\] = 1;
            }
            else{
                dir\[s1\[i\]\] +=1 ;
            }
        }
    }
    vector<PAIR> dir_vec(dir.begin(),dir.end());
    vector<PAIR>::iterator pos;
    sort(dir\_vec.begin(),dir\_vec.end(),cmp\_by\_value);
    cout<<*dir_vec.begin()<<endl;
    return 0;
}
```