---
title: Pat_1090（乙级）
url: 1804.html
id: 1804
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:32:10
tags:
  - pat
---

1090 危险品装箱 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1038429484026175488)

集装箱运输货物时，我们必须特别小心，不能把不相容的货物装在一只箱子里。比如氧化剂绝对不能跟易燃液体同箱，否则很容易造成爆炸。 本题给定一张不相容物品的清单，需要你检查每一张集装箱货品清单，判断它们是否能装在同一只箱子里。

### 输入格式：

输入第一行给出两个正整数：N (≤10​4​​) 是成对的不相容物品的对数；M (≤100) 是集装箱货品清单的单数。 随后数据分两大块给出。第一块有 N 行，每行给出一对不相容的物品。第二块有 M 行，每行给出一箱货物的清单，格式如下：

    K G[1] G[2] ... G[K]
    

其中 `K` (≤1000) 是物品件数，`G[i]` 是物品的编号。简单起见，每件物品用一个 5 位数的编号代表。两个数字之间用空格分隔。

### 输出格式：

对每箱货物清单，判断是否可以安全运输。如果没有不相容物品，则在一行中输出 `Yes`，否则输出 `No`。

### 输入样例：

    6 3
    20001 20002
    20003 20004
    20005 20006
    20003 20001
    20005 20004
    20004 20006
    4 00001 20004 00002 20003
    5 98823 20002 20003 20006 10010
    3 12345 67890 23333
    

### 输出样例：

    No
    Yes
    Yes

代码：
```
#include<iostream>
#include<map>
#include<vector>
#include<algorithm>
#include<cstdio>
//注意本题不要使用 string 作为map的key和value 这样会在测试点四种使用C++读取时会花费大量的时间导致超时 
//而是用int scanf则会大大缩短时间
using namespace std;

int main(){
    map<int,vector<int> > dir;
    //map<string,vector<string> >::iterator pos;
    int N,M;
    scanf("%d %d",&N,&M);
    //创建每个元素对应的不能够相容的名称列表
    for(int i=0;i<N;i++){
        int t1,t2;
        scanf("%d %d",&t1,&t2);
        dir\[t1\].push_back(t2);
        dir\[t2\].push_back(t1);
    }
    /*for(pos=dir.begin();pos!=dir.end();pos++){
        cout<<(*pos).first<<" : ";
        for(int i=0;i<((*pos).second).size();i++){
            cout<<((*pos).second)\[i\]<<" ";
        }
        cout<<endl;
    }*/
    for(int i=0;i<M;i++){
        bool flag = false;
        int num;
        scanf("%d",&num);
        vector<int> list1;
        for(int j=0;j<num;j++){
            int temp;
            scanf("%d",&temp);
            //遍历key值对应的value容器中是否存在于list1中如果存在则为No
            if(!flag){
                for(int k=0;k<dir\[temp\].size();k++){
                   if(count(list1.begin(),list1.end(),dir\[temp\]\[k\]) != 0){
                        flag = true;
                    }
                }
            }
            list1.push_back(temp);
        }
        if(flag){
            cout<<"No"<<endl;
        }
        else{
            cout<<"Yes"<<endl;
        }
    }
    return 0;
}
```