---
title: C++实现字母表全排序
url: 1194.html
id: 1194
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-05-15 23:22:16
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 全排列具体说明： 例如abc会有abc,acb,bac,bca,cab,abc六种情况 采用递归的方法： 先看a作为字母表首位时会有bc和cb两种排序 然后b作为字母表首位时会有ac和ca两种排序 最后是c作为字母表首位时会有ab和ba两种排序   这里就用到了swap（）进行交换。为了每次确保不重复， 第i个数分别与它后面的数字交换就能得到新的排列，这样可以构建一个递归   具体的代码：

#include<iostream>
#include<cstdio>
using namespace std;

//采用递归方式进行全排列
bool IsSwap(char *str, int Begin, int End)
{
    for (int i = Begin; i < End; i++)
        if (str\[i\] == str\[End\])
            return false;
    return true;
}
int num=1;
//k表示当前选取到第几个数,m表示共有多少数.
void AllRange(char *str, int k, int m)
{
    if (k == m)
    {
        static int s = 1;
        cout<<" 第"<<s++<<"个排列"<<str<<endl;;
    }
    else
    {
        for (int i = k; i <= m; i++) //第i个数分别与它后面的数字交换就能得到新的排列
        {
            if (IsSwap(str, k, i))
            {
                swap(*(str + k), *(str + i));
                AllRange(str, k + 1, m);
                swap(*(str + k), *(str + i));
            }
        }
    }
}


int main()
{
    int n=0;
    cout<<"输入你想要输出的个数：";
    cin>>n;
    char str\[100\]={'\\0'};  //最大容量为100
    for(int i =0;i<n;i++)
        cin>>str\[i\];
    str\[n\]='\\0';
    for(int i=1;i<=n;i++)
    {
        num=num*i;
    }
    cout<<"全排列总数个数为："<<num<<endl;
    AllRange(str, 0, n-1);
    return 0;
}

实现： ![](http://47.100.4.8/wp-content/uploads/2018/05/12314324324.png)