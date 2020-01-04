---
title: 贪婪算法C++实现
url: 665.html
id: 665
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-04-22 21:33:14
tags:
  - C/C++
  - Algorithm
  - 贪心算法
---

在介绍贪婪算法之前先介绍一下最优化问题。 每个最优化问题都包含一组限制条件和一个优化函数。符合限制条件的问题求解方案称为可行解。使优化函数可能取最佳值的可行解称为最优解。 贪婪算法： 在贪婪算法中，要逐步构造出一个最优解。每一步，我们都在一定的标准下，做出一个最有决策。在每一步做出的决策，在以后的步骤中都不可更改。作出决策所依据的标准称为贪婪准则。 下面用一个例子来阐述贪婪算法的思想以及对应的贪婪法则 找零钱：一个小孩用1美元来买价值不足1美元的糖果，售货员希望用数目最少的硬币找给小孩零钱。假设有面值为25美分，10美分，5美分和1美分的硬币，而且数目不限。售货员每次选择一枚硬币，凑成要找的零钱。 这里的选择硬币时的贪婪法则为：在不超过要找零钱数的情况下，每次尽可能选择面值最大的硬币。 假设要找给小孩66美分， 伪代码步骤：

1.  选择面值最大的硬币 和要找的钱数比较

if 面值最大的<要找的钱数比较： 选择该面值的硬币 else: 选择出它之外面值最大的硬币

2.  选择完成之后用当前要找的零钱数减去选择的面值的硬币，并在相应的计数上+1
3.  循环进行上面的步骤
4.  直至要找的钱凑够

  实现：
```
#include<iostream>
using namespace std;

int main()
{
    cout<<"零钱表：25美分，10美分，5美分，1美分若干个！"<<endl;
    int Con1 = 25;
    int Con2 = 10;
    int Con3 = 5;
    int Con4 = 1;
    cout<<"输入想要得找回的零钱数：(单位为美分)";
    int numCon = 0;
    cin>>numCon;
    int CountCon1=0,CountCon2=0,CountCon3=0,CountCon4 = 0;
    while(numCon != 0)
    {
        if(Con1 <= numCon)
        {
            CountCon1++;
            numCon = numCon - Con1;
        }
        else if(Con2 <= numCon)
        {
            CountCon2++;
            numCon = numCon - Con2;
        }
        else if(Con3 <= numCon)
        {
            CountCon3++;
            numCon = numCon - Con3;
        }
        else
        {
            CountCon4++;
            numCon = numCon - Con4;
        }
    }
    cout<<"需要25美分个数为:"<<CountCon1<<"个，需要10美分个数为:"
    <<CountCon2<<"个，需要5美分个数为："<<CountCon3<<"个，需要1美分个数为："<<CountCon4<<"个."<<endl;

    return 0;
}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/为3123.png)![](http://47.100.4.8/wp-content/uploads/2018/04/5214615315.png)