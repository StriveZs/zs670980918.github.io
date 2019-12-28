---
title: Pat_1020（乙级）
url: 1659.html
id: 1659
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:24:49
tags:
---

1020 月饼 （25 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805301562163200

月饼是中国人在中秋佳节时吃的一种传统食品，不同地区有许多不同风味的月饼。现给定所有种类月饼的库存量、总售价、以及市场的最大需求量，请你计算可以获得的最大收益是多少。 注意：销售时允许取出一部分库存。样例给出的情形是这样的：假如我们有 3 种月饼，其库存量分别为 18、15、10 万吨，总售价分别为 75、72、45 亿元。如果市场的最大需求量只有 20 万吨，那么我们最大收益策略应该是卖出全部 15 万吨第 2 种月饼、以及 5 万吨第 3 种月饼，获得 72 + 45/2 = 94.5（亿元）。

### 输入格式：

每个输入包含一个测试用例。每个测试用例先给出一个不超过 1000 的正整数 N 表示月饼的种类数、以及不超过 500（以万吨为单位）的正整数 D 表示市场最大需求量。随后一行给出 N 个正数表示每种月饼的库存量（以万吨为单位）；最后一行给出 N 个正数表示每种月饼的总售价（以亿元为单位）。数字间以空格分隔。

### 输出格式：

对每组测试用例，在一行中输出最大收益，以亿元为单位并精确到小数点后 2 位。

### 输入样例：

    3 20
    18 15 10
    75 72 45
    

### 输出样例：

    94.50

代码：（一直有一个测试点过不去的版本）应该是有些细节没注意到

#include<iostream>
#include<iomanip>

using namespace std;

int selectBest(double te\[\],int num){
    int index=0;
    double temp;
    temp = te\[0\];
    for(int i=0;i<num;i++){
        if(te\[i\]>=temp){
            index = i;
            temp = te\[i\];
        }
    }
    return index;
}

//考虑即使所有的都加起来也根本不满足最大值的情况
bool IsEmpty(double te\[\],int num){
    bool flag = true;
    for(int i=0;i<num;i++){
        if(te\[i\] != 0){
            flag = false;
        }
    }
    return flag;
}

int main(){
    int num,sum,index;
    cin>>num>>sum;
    int KuCun\[num\],ShouJia\[num\];
    double DanJia\[num\],money=0,temp=0;
    for(int i=0;i<num;i++){
        cin>>KuCun\[i\];
    }
    for(int i=0;i<num;i++){
        cin>>ShouJia\[i\];
    }
    for(int i=0;i<num;i++){
        DanJia\[i\] = double(ShouJia\[i\])/double(KuCun\[i\]);
        //cout<<DanJia\[i\]<<" ";
    }
    //cout<<endl;
    while(sum>0){
        if(IsEmpty(DanJia,num)){
            break;
        }
        //cout<<"1"<<endl;
        index = selectBest(DanJia,num);
        //cout<<index<<endl;
        DanJia\[index\] = 0;
        if(KuCun\[index\]<=sum){
            sum -= KuCun\[index\];
            money = money + ShouJia\[index\];
        }
        else{
            temp = double((double(sum)/double(KuCun\[index\]))*double(ShouJia\[index\]));
            money += temp;
            sum = 0;
        }
        //cout<<money<<endl;
    }
    cout<<setiosflags(ios::fixed)<<setprecision(2)<<money<<endl;
    return 0;
}

参考后改正的：

#include<bits/stdc++.h>
using namespace std;
struct mooncake
{
    double a;
    double b;
    double c;
} aa\[1100\];
bool cmp(mooncake n,mooncake m)
{
    return n.c>m.c;
}
int main()
{
    int n,m;
    cin>>n>>m;
    double sum=0;
    for(int i=0; i<n; i++)
        cin>>aa\[i\].a;
    for(int j=0; j<n; j++)
        cin>>aa\[j\].b;
    for(int i=0; i<n; i++)
        aa\[i\].c=aa\[i\].b/aa\[i\].a;
    sort(aa,aa+n,cmp);
    for(int i=0; i<n; i++)
    {
        if(aa\[i\].a<=m)
        {
            m-=aa\[i\].a;
            sum+=aa\[i\].b;
        }
        else if(aa\[i\].a>m)
        {
            sum+=aa\[i\].c*m;
            break;
        }
    }
    printf("%.2f\\n",sum);
    return 0;
}