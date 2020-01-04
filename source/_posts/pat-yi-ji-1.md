---
title: Pat_1035（乙级）
url: 1690.html
id: 1690
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:54:54
tags:
  - pat
---

1035 插入与归并 （25 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805286714327040)

关于归并排序的代码后面给出，思路主要是先进行归并排序的判断如果不是那么对于插入排序的判断就比较简单实现了，只需要比较和之前数列的差距即可。 根据维基百科的定义： **插入排序**是迭代算法，逐一获得输入数据，逐步产生有序的输出序列。每步迭代中，算法从输入序列中取出一元素，将之插入有序序列中正确的位置。如此迭代直到全部元素有序。 **归并排序**进行如下迭代操作：首先将原始序列看成 N 个只包含 1 个元素的有序子序列，然后每次迭代归并两个相邻的有序子序列，直到最后只剩下 1 个有序的序列。 现给定原始序列和由某排序算法产生的中间序列，请你判断该算法究竟是哪种排序算法？

### 输入格式：

输入在第一行给出正整数 N (≤100)；随后一行给出原始序列的 N 个整数；最后一行给出由某排序算法产生的中间序列。这里假设排序的目标序列是升序。数字间以空格分隔。

### 输出格式：

首先在第 1 行中输出`Insertion Sort`表示插入排序、或`Merge Sort`表示归并排序；然后在第 2 行中输出用该排序算法再迭代一轮的结果序列。题目保证每组测试的结果是唯一的。数字间以空格分隔，且行首尾不得有多余空格。

### 输入样例 1：

    10
    3 1 2 8 7 5 9 4 6 0
    1 2 3 7 8 5 9 4 6 0
    

### 输出样例 1：

    Insertion Sort
    1 2 3 5 7 8 9 4 6 0
    

### 输入样例 2：

    10
    3 1 2 8 7 5 9 4 0 6
    1 3 2 8 5 7 4 9 0 6
    

### 输出样例 2：

    Merge Sort
    1 2 3 8 4 5 7 9 0 6

代码：
```
#include<iostream>
#include<algorithm>

using namespace std;

//判断是否相等
bool IsEque(int a\[\],int b\[\],int num){
    bool flag = true;
    for(int m=0;m<num;m++){
        if(a\[m\] != b\[m\]){
            flag = false;
            break;
        }
    }
    return flag;
}
//归并排序
bool merge_sort(int \*init,int \*target,int num){
    bool flag = false;
    int step = 2;
    while(step<num){
        int index = 0;
        while(true){
            if(index + step >= num){
                sort(init+index,init+num,less<int>());
                break;
            }
            else{
                sort(init+index,init+index+step,less<int>());
                index += step;
            }
        }
        if(IsEque(init,target,num)){
            flag = true;
            index = 0;
            step = step * 2;
            cout<<"Merge Sort"<<endl;
            while(true){
                if(index + step >= num){
                    sort(init+index,init+num,less<int>());
                    break;
                }
                else{
                    sort(init+index,init+index+step,less<int>());
                    index += step;
                }
            }
            for(int i=0;i<num;i++){
                if(i == num-1){
                    cout<<init\[i\];
                }
                else{
                    cout<<init\[i\]<<" ";
                }
            }
            break;
        }
        step = step * 2;
    }
    return flag;
}
//插入排序
void insert_sort(int \*init,int \*target,int num){
    int index=0;
    for(int i=1;i<num;i++){
        if(target\[index\]<=target\[i\]){
            index++;
        }
        else{
            index++;
            break;
        }
    }
    cout<<"Insertion Sort"<<endl;
    sort(target,target+index+1,less<int>());
    for(int i=0;i<num;i++){
        if(i == num-1){
            cout<<target\[i\];
        }
        else{
            cout<<target\[i\]<<" ";
        }
    }

}

int main(){
    int num;
    cin>>num;
    int init\[num\],target\[num\],backup\[num\];
    for(int i=0;i<num;i++){
        cin>>init\[i\];
        backup\[i\] = init\[i\];
    }
    for(int i=0;i<num;i++){
        cin>>target\[i\];
    }
    bool flag = merge_sort(init,target,num);
    if(!flag){
        insert_sort(init,target,num);
    }
    return 0;
}
```