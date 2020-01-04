---
title: Pat_1025（乙级）
url: 1669.html
id: 1669
categories:
  - PAT
  - 乙级
date: 2019-03-12 11:36:11
tags:
  - pat
---

1025 反转链表 （25 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805296180871168)

给定一个常数 K 以及一个单链表 L，请编写程序将 L 中每 K 个结点反转。例如：给定 L 为 1→2→3→4→5→6，K 为 3，则输出应该为 3→2→1→6→5→4；如果 K 为 4，则输出应该为 4→3→2→1→5→6，即最后不到 K 个元素不反转。

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例第 1 行给出第 1 个结点的地址、结点总个数正整数 N (≤10​5​​)、以及正整数 K (≤N)，即要求反转的子链结点的个数。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。 接下来有 N 行，每行格式为：

    Address Data Next
    

其中 `Address` 是结点地址，`Data` 是该结点保存的整数数据，`Next` 是下一结点的地址。

### 输出格式：

对每个测试用例，顺序输出反转后的链表，其上每个结点占一行，格式与输入相同。

### 输入样例：

    00100 6 4
    00000 4 99999
    00100 1 12309
    68237 6 -1
    33218 3 00000
    99999 5 68237
    12309 2 33218
    

### 输出样例：

    00000 4 33218
    33218 3 12309
    12309 2 00100
    00100 1 99999
    99999 5 68237
    68237 6 -1

代码：
```
#include<iostream>
#include<map>
#include<algorithm>

/*这里一定要注意 对于链表的排序 一定不能使用排序算法  应该采用map类似字典的方式去寻找下一个节点
对于逆序的话则是采用reverse来进行高效的逆置*/
using namespace std;

struct Node{
    string address;
    int data;
    string next;
};

void sorted(Node nodes\[\],int num){
    string s1,s2;
    int t;
    for(int i=0;i<num-1;i++){
        for(int j = i+1;j<num;j++){
            if(nodes\[i\].next == nodes\[j\].address){
                s1 = nodes\[i+1\].address;
                t = nodes\[i+1\].data;
                s2 = nodes\[i+1\].next;
                nodes\[i+1\].address = nodes\[j\].address;
                nodes\[i+1\].data = nodes\[j\].data;
                nodes\[i+1\].next = nodes\[j\].next;
                nodes\[j\].address = s1;
                nodes\[j\].data = t;
                nodes\[j\].next = s2;
            }
        }
    }
}

int main(){
    map<string,Node> qwe;
    string start;
    int num,temp;
    cin>>start>>num>>temp;
    Node nodes\[num\];
    for(int i=0;i<num;i++){
        string s1,s2,s3,s4;
        int t,t1;
        cin>>s1>>t>>s2;
        qwe\[s1\].data = t;
        qwe\[s1\].next = s2;
    }
    int num1=0;
    for(int i=0;i<num;i++){
        nodes\[i\] = {start,qwe\[start\].data,"0"};
        start = qwe\[start\].next;
        if(start == "-1"){
            num1 = i+1;
            break;
        }
    }
    //sorted(nodes,num);
    /*cout<<endl;
    for(int i=0;i<num1;i++){
        cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" "<<nodes\[i\].next<<endl;
    }
    cout<<endl;*/
    if(temp > num1){ //不足temp个的情况
        for(int i=0;i<num1;i++){
            cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" "<<nodes\[i\].next<<endl;
        }
    }
    else if(temp == num1){
        reverse(nodes,nodes+num1);
        for(int i=0;i<num1;i++){
            if(i == num1-1){
                cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" -1"<<endl;
            }
            else{
                cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" "<<nodes\[i+1\].address<<endl;
            }
        }
    }
    else{
        int sum,rez,m,n,step=0;
        sum = num1 / temp; //总共sum次反转
        rez = num1 % temp; //剩余rez个不反转
        for(int i=0;i<sum;i++){
            m = i * temp;
            n = (i + 1) * temp;
            reverse(nodes+m,nodes+n);
        }
        for(int i=0;i<num1;i++){
            if(i == num1-1){
                cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" -1"<<endl;
            }
            else{
                cout<<nodes\[i\].address<<" "<<nodes\[i\].data<<" "<<nodes\[i+1\].address<<endl;
            }
        }
    }
}
```