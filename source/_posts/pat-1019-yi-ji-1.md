---
title: Pat_1019（乙级）
url: 1657.html
id: 1657
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:22:36
tags:
  - pat
---

1019 数字黑洞 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805302786899968

给定任一个各位数字不完全相同的 4 位正整数，如果我们先把 4 个数字按非递增排序，再按非递减排序，然后用第 1 个数字减第 2 个数字，将得到一个新的数字。一直重复这样做，我们很快会停在有“数字黑洞”之称的 `6174`，这个神奇的数字也叫 Kaprekar 常数。 例如，我们从`6767`开始，将得到

    7766 - 6677 = 1089
    9810 - 0189 = 9621
    9621 - 1269 = 8352
    8532 - 2358 = 6174
    7641 - 1467 = 6174
    ... ...
    

现给定任意 4 位正整数，请编写程序演示到达黑洞的过程。

### 输入格式：

输入给出一个 (0,10​4​​) 区间内的正整数 N。

### 输出格式：

如果 N 的 4 位数字全相等，则在一行内输出 `N - N = 0000`；否则将计算的每一步在一行内输出，直到 `6174` 作为差出现，输出格式见样例。注意每个数字按 `4` 位数格式输出。

### 输入样例 1：

    6767
    

### 输出样例 1：

    7766 - 6677 = 1089
    9810 - 0189 = 9621
    9621 - 1269 = 8352
    8532 - 2358 = 6174
    

### 输入样例 2：

    2222
    

### 输出样例 2：

    2222 - 2222 = 0000

代码：
```
#include<iostream>
#include<iomanip>
#include<algorithm>
using namespace std;
bool cmp(int a,int b)//设计函数以降序 
{
	return a>b;
}
int GetNum(int *a)//将数组内的元素转为数字 
{
	int sum=0;
	for(int i=0;i<4;i++)
	sum=sum*10+a\[i\];
	return sum;
}
void Clear(int *a)//清空数组内的元素，即将数组内的元素置0 
{
	for(int i=0;i<4;i++)
	a\[i\]=0;
}
void StoreNum(int *a,int n)//将数字存储至数组中 
{
	int i=0;
	while(n)
	{
		a\[i++\]=n%10;
		n/=10;	
	}
}
void OutPut(int *a)
{
	int n1,n2,n;
	do
	{
		sort(a,a+4,cmp);//降序 
		n1=GetNum(a);
		cout<<setw(4)<<setfill('0')<<right<<n1<<" - ";
		sort(a,a+4);//升序 
		n2=GetNum(a);
		n=n1-n2;
		cout<<setw(4)<<setfill('0')<<right<<n2<<" = ";
		cout<<setw(4)<<setfill('0')<<right<<n<<'\\n';
		Clear(a);//清空 
		StoreNum(a,n);//存储差 
	}while(n!=6174);
}
int main()
{
	int N,a\[4\]={0},i=0;//定义存储数字的数组,初始化元素都为0 
	cin>>N;
	StoreNum(a,N);
	if(a\[0\]==a\[1\]&&a\[0\]==a\[2\]&&a\[0\]==a\[3\])
	{
		cout<<a\[0\]<<a\[0\]<<a\[0\]<<a\[0\]<<" - "<<a\[0\]<<a\[0\]<<a\[0\]<<a\[0\];
		cout<<" = 0000";
	}
	else 
	OutPut(a);
	return 0;
}
```