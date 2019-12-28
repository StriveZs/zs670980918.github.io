---
title: Pat_1003（乙级）
url: 1625.html
id: 1625
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:52:07
tags:
---

1003 我要通过！ （20 分）  地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805323154440192

“**答案正确**”是自动判题系统给出的最令人欢喜的回复。本题属于 PAT 的“**答案正确**”大派送 —— 只要读入的字符串满足下列条件，系统就输出“**答案正确**”，否则输出“**答案错误**”。 得到“**答案正确**”的条件是：

1.  字符串中必须仅有 `P`、 `A`、 `T`这三种字符，不可以包含其它字符；
2.  任意形如 `xPATx` 的字符串都可以获得“**答案正确**”，其中 `x` 或者是空字符串，或者是仅由字母 `A` 组成的字符串；
3.  如果 `aPbTc` 是正确的，那么 `aPbATca` 也是正确的，其中 `a`、 `b`、 `c` 均或者是空字符串，或者是仅由字母 `A` 组成的字符串。

现在就请你为 PAT 写一个自动裁判程序，判定哪些字符串是可以获得“**答案正确**”的。

### 输入格式：

每个测试输入包含 1 个测试用例。第 1 行给出一个正整数 n (<10)，是需要检测的字符串个数。接下来每个字符串占一行，字符串长度不超过 100，且不包含空格。

### 输出格式：

每个字符串的检测结果占一行，如果该字符串可以获得“**答案正确**”，则输出 `YES`，否则输出 `NO`。

### 输入样例：

    8
    PAT
    PAAT
    AAPATAA
    AAPAATAAAA
    xPATx
    PT
    Whatever
    APAAATAA
    

### 输出样例：

    YES
    YES
    YES
    YES
    NO
    NO
    NO
    NO

代码：

#include <stdio.h>
#include <iostream>
#include <string.h>
#include <string>
#include <sstream>

using namespace std;

int main(){
    int n;
    char c\[101\];
    scanf("%d", &n);
    for(int i=0;i<n;i++){
        bool result = true;
        int count1 = 0, count2 = 0, count3 = 0;
        int countP = 0, countT = 0;
        scanf("%s", c);
        for(int j=0;j<strlen(c);j++){
            if(c\[j\] != 'P' && c\[j\] != 'A' && c\[j\] != 'T'){
                result = false;
                break;
            }
            if(c\[j\] == 'P'){
                countP ++;
                if(countP == 2){
                    result = false;
                    break;
                }
            }
            if(c\[j\] == 'T'){
                countT ++;
                if(countT == 2){
                    result = false;
                    break;
                }
            }
        }
        if(result){
            string s = c;
            count1 = s.find("P");
            count2 = s.find("A");
            count3 = s.find("T");
            if(count1 == -1 || count2 == -1 || count3 == -1){
                result = false;
            }
            else{
                result = ((count1 * (count3 - count1 - 1)) == (strlen(c) - count3 - 1)) ? true : false;
            }
        }
        if(result){
            printf("YES\\n");
        }
        else{
            printf("NO\\n");
        }
    }
    return 0;
}