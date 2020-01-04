---
title: C++ 实现大数的加减乘除
url: 1609.html
id: 1609
categories:
  - C&amp;C++
  - C++学习
  - 文章页
  - 算法
date: 2019-02-07 12:16:46
tags:
  - 大数加减乘除
---

这里采用了string来存储大数，其实之前还考虑了使用数组来存储但是感觉操作不如string所以最终还是采用了string来存储。 1.大数的加法： 核心思想：主要是将两个大数逐位相加（从低位到高），若相加的结果大于10则采用取余的方法来得到当前位的值，然后使用除来得到进位。 代码：
```
#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

string BigNumberAdd(){
    string s1,s2,result(10000,'0');
    cin>>s1>>s2;
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    for(int i=0;i<s1.length();i++){
        result\[i\] = s1\[i\];
    }
    int temp = 0;
    for(int i=0;i<s2.length();i++){
        temp += (result\[i\]-'0' + s2\[i\] -'0');
        result\[i\] = temp%10 + '0';
        temp /= 10;
    }
    result\[s2.length()\] = (result\[s2.length()\]-'0') + temp + '0';
    reverse(result.begin(),result.end());
    return result.substr(result.find\_first\_not_of('0'));
}
int main(){
    string result;
    result = BigNumberAdd();
    cout<<result<<endl;
    return 0;
}

2.大数的减法 核心思想：首先要注意的是要保证是大数减小数（都是绝对值），然后在结果出添加适当的负号即可，从低位到高位逐位相减，如果不够则从前以为借位然后加10在相减。特别要注意对相等情况的处理（在这里被坑了因为后面除法时也用到了减法 咕~QAQ） 代码：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

bool getBiggerOne(string s1,string s2){
    bool flag = false;
    if(s1.length() > s2.length()){
        return flag;
    }
    else if(s1.length() < s2.length()){
        flag = true;
        return flag;
    }
    else{
        for(int i=0;i<s1.length();i++){
            if(s1\[i\] != s2\[i\]){
                int temp1,temp2;
                temp1 = s1\[i\] - '0';
                temp2 = s2\[i\] - '0';
                if(temp1 > temp2){
                    return false;
                }
                else{
                    return true;
                }
            }
        }
    }
}

string BigNumberJian(){
    string s1,s2,result(10000,'0');
    cin>>s1>>s2;
    if(s1 == s2){
        return "0";
    }
    bool flag = getBiggerOne(s1,s2);
    if(flag){
        swap(s1,s2);
        //cout<<"3"<<endl;
    }
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    //cout<<s1<<" "<<s2<<endl;
    for(int i=0;i<s1.length();i++){
        result\[i\] = s1\[i\];
    }
    for(int i=0;i<s2.length();i++){
        int temp1,temp2;
        //cout<<"1"<<endl;
        temp1 = result\[i\] - '0';
        temp2 = s2\[i\] - '0';
        if(temp1 >= temp2){
            //cout<<"1"<<endl;
            result\[i\] = temp1 - temp2 + '0';
        }
        else{
            //cout<<"2"<<endl;
            result\[i+1\] = result\[i+1\] - '0' - 1 + '0';
            result\[i\] = result\[i\] - '0' + 10 - (s2\[i\]-'0') + '0';
        }
    }
    reverse(result.begin(),result.end());
    result = result.substr(result.find\_first\_not_of('0'));
    //负号判断
    if(flag){
        reverse(result.begin(),result.end());
        result += '-';
        reverse(result.begin(),result.end());
    }
    return result;
}

int main(){
    string result;
    result = BigNumberJian();
    cout<<result<<endl;
}

  3.大数的乘法 核心思想：这里主要参考了Comba乘法原理，具体这里：[https://www.cnblogs.com/starrybird/p/4419444.html](https://www.cnblogs.com/starrybird/p/4419444.html) 大体上的乘法过程同样是基于笔算乘法的思路来进行的，只不过先不考虑进位，先将每一行乘出来，然后将每一列加起来然后求取得到当前位的值并且使用除的来得到进位。 ![](http://47.100.4.8/wp-content/uploads/2019/02/QQ图片20190207122305.png)   代码：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

string BigNumberMult(){
    string s1,s2,s(10000,'0');
    cin>>s1>>s2;
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
int main(){
    string result;
    result = BigNumberMult();
    cout<<result<<endl;
    return 0;
}

4.大数的除法（这里用到了之前编写的大数减法） 核心思想：这里主要是使用相减来得到最后的商和余数的，如 22 -20 =2 由于减了一次所以商是1 余数为2  但是若为333333 - 3 则要进行很多次减法运算，这样时空复杂度都会大大的提高，所以这里采用补0的减法，如：222 - 3 可以先进行 222 - 300 得到一个负数 则最高位为0，然后进行222 - 30 进行了7次相减 则次高位为7 然后用减完的数再次进行 减法 12 -3 进行了4次相减 所以得到了商为74。 代码：

#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

bool getBiggerOne(string s1,string s2){
    bool flag = false;
    if(s1.length() > s2.length()){
        return flag;
    }
    else if(s1.length() < s2.length()){
        flag = true;
        return flag;
    }
    else{
        for(int i=0;i<s1.length();i++){
            if(s1\[i\] != s2\[i\]){
                int temp1,temp2;
                temp1 = s1\[i\] - '0';
                temp2 = s2\[i\] - '0';
                if(temp1 > temp2){
                    return false;
                }
                else{
                    return true;
                }
            }
        }
    }
}

string BigNumberJian(){
    string s1,s2,result(10000,'0');
    cin>>s1>>s2;
    if(s1 == s2){
        return "0";
    }
    bool flag = getBiggerOne(s1,s2);
    if(flag){
        swap(s1,s2);
        //cout<<"3"<<endl;
    }
    reverse(s1.begin(),s1.end());
    reverse(s2.begin(),s2.end());
    //cout<<s1<<" "<<s2<<endl;
    for(int i=0;i<s1.length();i++){
        result\[i\] = s1\[i\];
    }
    for(int i=0;i<s2.length();i++){
        int temp1,temp2;
        //cout<<"1"<<endl;
        temp1 = result\[i\] - '0';
        temp2 = s2\[i\] - '0';
        if(temp1 >= temp2){
            //cout<<"1"<<endl;
            result\[i\] = temp1 - temp2 + '0';
        }
        else{
            //cout<<"2"<<endl;
            result\[i+1\] = result\[i+1\] - '0' - 1 + '0';
            result\[i\] = result\[i\] - '0' + 10 - (s2\[i\]-'0') + '0';
        }
    }
    reverse(result.begin(),result.end());
    result = result.substr(result.find\_first\_not_of('0'));
    //负号判断
    if(flag){
        reverse(result.begin(),result.end());
        result += '-';
        reverse(result.begin(),result.end());
    }
    return result;
}

int main(){
    string result;
    result = BigNumberJian();
    cout<<result<<endl;
}
```