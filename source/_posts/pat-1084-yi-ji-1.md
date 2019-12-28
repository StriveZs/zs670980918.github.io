---
title: Pat_1084（乙级）
url: 1792.html
id: 1792
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:23:59
tags:
---

1084 外观数列 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805260583813120)

外观数列是指具有以下特点的整数序列：

    d, d1, d111, d113, d11231, d112213111, ...
    

它从不等于 1 的数字 `d` 开始，序列的第 n+1 项是对第 n 项的描述。比如第 2 项表示第 1 项有 1 个 `d`，所以就是 `d1`；第 2 项是 1 个 `d`（对应 `d1`）和 1 个 1（对应 11），所以第 3 项就是 `d111`。又比如第 4 项是 `d113`，其描述就是 1 个 `d`，2 个 1，1 个 3，所以下一项就是 `d11231`。当然这个定义对 `d` = 1 也成立。本题要求你推算任意给定数字 `d` 的外观数列的第 N 项。

### 输入格式：

输入第一行给出 \[0,9\] 范围内的一个整数 `d`、以及一个正整数 N（≤ 40），用空格分隔。

### 输出格式：

在一行中给出数字 `d` 的外观数列的第 N 项。

### 输入样例：

    1 8
    

### 输出样例：

    1123123111

代码：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;
//题目理解 是对于 d为第一项 则第二项就为d1（其中1）表示有一个d 第三项（针对第二项）就为d1（有一个d）11（有一个1）以此类推
//同样要注意 这里每次统计的是连续的相同的字符个数
//算法思想：从头到尾遍历字符串然后统计个数并添加到对应的数值后面之后下一次从上次统计结束的地方开始统计
int main(){
    string d;
    int num;
    cin>>d>>num;
    num--;
    //因为算法中先减了1所以对于 N等于1的情况要特殊处理
    if(num == 0){
        cout<<d<<endl;
        return 0;
    }
    string result = d + "1";
    while(num > 1){
        string s1="";
        int index = 0;
        while(index < result.length()){
            bool flag = true;
            int num1 = 1;
            int j;
            char temp = result\[index\];
            s1 += result\[index++\];
            for(j=index;j<result.length();j++){
                if(temp != result\[j\]){
                    index = j;
                    flag  = false;
                    break;
                }
                else{
                    num1++;
                }
            }
            if(flag){ //如果全相等（如1111）则不会break 只会正常结束 因此要再次进行index赋值 否则不会按照统计后的位置进行
                index = j;
            }
            s1 += (num1 + '0');
        }
        result = s1;
        num--;
    }
    cout<<result<<endl;
    return 0;
}