---
title: Pat_1012（乙级）
url: 1643.html
id: 1643
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:04:34
tags:
---

1012 数字分类 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805311146147840

给定一系列正整数，请按要求对数字进行分类，并输出以下 5 个数字：

*   A​1​​ = 能被 5 整除的数字中所有偶数的和；
*   A​2​​ = 将被 5 除后余 1 的数字按给出顺序进行交错求和，即计算 n​1​​−n​2​​+n​3​​−n​4​​⋯；
*   A​3​​ = 被 5 除后余 2 的数字的个数；
*   A​4​​ = 被 5 除后余 3 的数字的平均数，精确到小数点后 1 位；
*   A​5​​ = 被 5 除后余 4 的数字中最大数字。

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例先给出一个不超过 1000 的正整数 N，随后给出 N 个不超过 1000 的待分类的正整数。数字间以空格分隔。

### 输出格式：

对给定的 N 个正整数，按题目要求计算 A​1​​~A​5​​ 并在一行中顺序输出。数字间以空格分隔，但行末不得有多余空格。 若其中某一类数字不存在，则在相应位置输出 `N`。

### 输入样例 1：

    13 1 2 3 4 5 6 7 8 9 10 20 16 18
    

### 输出样例 1：

    30 11 2 9.7 9
    

### 输入样例 2：

    8 1 2 4 5 6 7 9 16
    

### 输出样例 2：

    N 11 2 N 9

代码：（有一个测试点一直通不过）

#include<iostream>
#include<iomanip>

using namespace std;

int main(){
    int qwe,temp,num=0,A1=0,A2=0,A3=0,A5=0,sum=0,r1=0,r2=0;
    float A4=0,t=0;
    cin>>qwe;
    while(qwe>0){
        qwe--;
        cin>>temp;
        r1 = temp/5;
        r2 = temp - r1*5;
        if(r2==0 && temp%2==0){
            A1 += temp;
        }
        else if(r2==1){
            if(num%2==0){
                A2 += temp;
                num++;
            }
            else{
                A2 -= temp;
                num++;
            }
        }
        else if(r2==2){
            A3++;
        }
        else if(r2==3){
            A4 += temp;
            t++;
        }
        else if(r2==4){
            if(temp>A5){
                A5=temp;
            }
        }
        else{
            sum++;
        }

    }
    if(A1 == 0){
        cout<<"N ";
    }
    else{
        cout<<A1<<" ";
    }
    if(A2 == 0){
        cout<<"N ";
    }
    else{
        cout<<A2<<" ";
    }
    if(A3 == 0){
        cout<<"N ";
    }
    else{
        cout<<A3<<" ";
    }
    if(A4 == 0){
        cout<<"N ";
    }
    else{
        float q = A4/t;
        cout<<setiosflags(ios::fixed)<<setprecision(1)<<q<<" ";
    }
    if(A5 == 0){
        cout<<"N"<<endl;
    }
    else{
        cout<<A5<<endl;
    }
    return 0;
}

参考别人后改正的：

#include<iostream>
#include<iomanip>
#include<typeinfo>

using namespace std;

int main()
{
    int N, A\[5\] = { 0 }, j = 1, num = 0, max = 0, dig\[5\] = { 0 };

    cin >> N;

    int *p = new int\[N\];

    for (int i = 0; i < N; i++)
    {
        cin >> p\[i\];

        switch (p\[i\] % 5)
        {
        case 0:
            if ((p\[i\] & 1) == 0)
            {
                A\[0\] += p\[i\];
                dig\[0\] = 1;
            }
            break;
        case 1:
            A\[1\] += p\[i\] * j;
            j = -j;
            dig\[1\] = 1;
            break;
        case 2:
            A\[2\]++;
            dig\[2\] = 1;
            break;
        case 3:
            A\[3\] += p\[i\];
            num++;
            dig\[3\] = 1;
            break;
        case 4:
            if (p\[i\] > max)
                max = p\[i\];
            dig\[4\] = 1;
            break;
        default:break;
        }
    }

    A\[4\] = max;

    for (int i = 0; i < 5; i++)
    {
        if (dig\[i\])
        {
            if (i != 3)
                cout << A\[i\];
            else
                cout << fixed << setprecision(1) << static_cast<double>(A\[3\]) / num;
        }
        else
            cout << "N";

        if (i != 4)
            cout << " ";
    }

    delete\[\] p;

    return 0;
}