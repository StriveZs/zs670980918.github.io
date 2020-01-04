---
title: Pat_1091（乙级）
url: 1806.html
id: 1806
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:33:20
tags:
  - pat
---

1091 N-自守数 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1071785664454127616)

如果某个数 K 的平方乘以 N 以后，结果的末尾几位数等于 K，那么就称这个数为“N-自守数”。例如 3×92​2​​=25392，而 25392 的末尾两位正好是 92，所以 92 是一个 3-自守数。 本题就请你编写程序判断一个给定的数字是否关于某个 N 是 N-自守数。

### 输入格式：

输入在第一行中给出正整数 M（≤20），随后一行给出 M 个待检测的、不超过 1000 的正整数。

### 输出格式：

对每个需要检测的数字，如果它是 N-自守数就在一行中输出最小的 N 和 NK​2​​ 的值，以一个空格隔开；否则输出 `No`。注意题目保证 N<10。

### 输入样例：

    3
    92 5 233
    

### 输出样例：

    3 25392
    1 25
    No

代码：
```
#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;
//思想：这里采用了大数乘法 按照题目要求计算result 然后使用reverse进行结果逆转 然后使用find进行匹配如果为0则证明以temp结尾
string BigNumberMult(string s1,string s2){
    string s(10000,'0');
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    for(int i=0;i<s1.length();i++){
        for(int j=0;j<s2.length();j++){
            int temp = (s1\[i\] - '0') * (s2\[j\] - '0');
            s\[i+j+1\] = s\[i+j+1\] - '0' + (s\[i+j\] - '0' + temp) / 10 + '0';
            s\[i+j\] = (s\[i+j\] - '0' + temp) % 10 + '0';
        }
    }
    reverse(s.begin(),s.end());
    if(s.find\_first\_not_of('0') == string::npos){
        return "0";
    }
    else{
        return s.substr(s.find\_first\_not_of('0'));
    }
}
//匹配函数
bool judge(string s1,string s2){
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    if(s1.find(s2) == 0){
        return true;
    }
    return false;
}

int main(){
    int num;
    cin>>num;
    string tt\[num\];
    for(int i=0;i<num;i++){
        cin>>tt\[i\];
    }
    for(int i=0;i<num;i++){
        string temp,result;
        temp = BigNumberMult(tt\[i\],tt\[i\]);
        result = temp;
        int counts = 0;
        bool flag = true;
        while(counts < 10){
            string t = "";
            t += (counts + 1 + '0');
            result = BigNumberMult(temp,t);
            if(judge(result,tt\[i\])){
                flag = false;
                break;
            }
            counts++;
        }
        if(flag){
            cout<<"No"<<endl;
        }
        else{
            cout<<counts+1<<" "<<result<<endl;
        }
    }
    return 0;
}
```