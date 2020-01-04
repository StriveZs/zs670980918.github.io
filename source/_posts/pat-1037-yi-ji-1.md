---
title: Pat_1037（乙级）
url: 1696.html
id: 1696
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:11:08
tags:
  - pat
---

1037 在霍格沃茨找零钱 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805284923359232)

如果你是哈利·波特迷，你会知道魔法世界有它自己的货币系统 —— 就如海格告诉哈利的：“十七个银西可(Sickle)兑一个加隆(Galleon)，二十九个纳特(Knut)兑一个西可，很容易。”现在，给定哈利应付的价钱 P 和他实付的钱 A，你的任务是写一个程序来计算他应该被找的零钱。

### 输入格式：

输入在 1 行中分别给出 P 和 A，格式为 `Galleon.Sickle.Knut`，其间用 1 个空格分隔。这里 `Galleon` 是 \[0, 10​7​​\] 区间内的整数，`Sickle` 是 \[0, 17) 区间内的整数，`Knut` 是 \[0, 29) 区间内的整数。

### 输出格式：

在一行中用与输入同样的格式输出哈利应该被找的零钱。如果他没带够钱，那么输出的应该是负数。

### 输入样例 1：

    10.16.27 14.1.28
    

### 输出样例 1：

    3.2.1
    

### 输入样例 2：

    14.1.28 10.16.27
    

### 输出样例 2：

    -3.2.1

代码：
```
#include <cstdio>
#include <cstdlib>
#include <cstring>
//思路：将所有钱转换为最小的单位 然后减完之后在换算回去
const int Galleon = 17 * 29;
const int Sickle  = 29;

int main(int argc, char const *argv\[\])
{
    int a1, b1, c1;
    int a2, b2, c2;
    scanf("%d.%d.%d %d.%d.%d", &a1, &b1, &c1, &a2, &b2, &c2 );
    int price = a1 * Galleon + b1 * Sickle + c1;
    int money = a2 * Galleon + b2 * Sickle + c2;
    int change = money - price; //找零的钱
    if(change < 0)
    {
        printf("-");
        change = -change;
    }
    printf("%d.%d.%d\\n", change / Galleon, change % Galleon / Sickle, change % Sickle);

    return 0;
}
```