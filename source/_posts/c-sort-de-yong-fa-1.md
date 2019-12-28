---
title: C++ sort的用法
url: 1605.html
id: 1605
categories:
  - C&amp;C++
  - C++学习
  - 文章页
  - 算法
date: 2019-02-04 11:23:31
tags:
---

**sort类函数：**

[函数名](http://www.stlchina.org/twiki/bin/view.pl/Main/STLSortAlgorithms?sortcol=0&table=1&up=0#sorted_table "Sort by this column")

[功能描述](http://www.stlchina.org/twiki/bin/view.pl/Main/STLSortAlgorithms?sortcol=1&table=1&up=0#sorted_table "Sort by this column")

sort

对给定区间所有元素进行排序

stable_sort

对给定区间所有元素进行稳定排序

partial_sort

对给定区间所有元素部分排序

partial\_sort\_copy

对给定区间复制并排序

nth_element

找出给定区间的某个位置对应的元素

is_sorted

判断一个区间是否已经排好序

partition

使得符合某个条件的元素放在前面

stable_partition

相对稳定的使得符合某个条件的元素放在前面

需要头文件<algorithm> 语法描述：sort（begin，end，cmp），cmp参数可以没有，如果没有默认非降序排序。 其实对于这么简单的任务（类型支持“<”、“>”等比较运算符），完全没必要自己写一个类出来。标准库里已经有现成的了，就在functional里，include进来就行了。functional提供了一堆基于模板的比较函数对象。它们是（看名字就知道意思了）：equal\_to<Type>、not\_equal\_to<Type>、greater<Type>、greater\_equal<Type>、less<Type>、less_equal<Type>。对于这个问题来说，greater和less就足够了，直接拿过来用：

*   升序：sort(begin,end,less<data-type>());
*   降序：sort(begin,end,greater<data-type>())

例如（对整形排序为例）：

#include<iostream>
#include<algorithm>

using namespace std;

int main(){
    int temp\[10\],j;
    for(int i=0;i<10;i++){
        cin>>j;
        temp\[i\] = j;
    }
    sort(temp,temp+10,greater<int>());
    for(int i=0;i<10;i++){
        cout<<temp\[i\]<<" ";
    }
    return 0;
}

降序同理， ![](http://47.100.4.8/wp-content/uploads/2019/02/QQ图片20190204111753.png)   下面是自己手动编写cmp来设置排序规则： 以下面这道例题为例来进行编写（对结构体排序）： 输入第一行给出 3 个正整数，分别为：N（≤10​5​​），即考生总数；L（≥60），为录取最低分数线，即德分和才分均不低于 L 的考生才有资格被考虑录取；H（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于 H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线 L 的考生也按总分排序，但排在第三类考生之后。 随后 N 行，每行给出一位考生的信息，包括：`准考证号 德分 才分`，其中`准考证号`为 8 位整数，德才分为区间 \[0, 100\] 内的整数。数字间以空格分隔。 输出第一行首先给出达到最低分数线的考生人数 M，随后 M 行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。 代码：

#include<iostream>
#include<algorithm>
#include<deque>

using namespace std;

struct mess{
    int ID;
    int De;
    int Cai;
    int Zong;
};

bool cmp2(mess a,mess b){
    if(a.Zong != b.Zong){
        return a.Zong>b.Zong;
    }
    else{
        if(a.De != b.De){
            return a.De>b.De;
        }
        else{
            return a.ID<b.ID;
        }
    }
}

int main(){
    int num,low,better,temp1,temp2,temp3,sum=0;
    cin>>num>>low>>better;
    mess student\[num\];
    deque<mess> first_level;
    deque<mess> second_level;
    deque<mess> third_level;
    deque<mess> forst_level;
    deque<mess>::iterator pos;
    for(int i=0;i<num;i++){
        cin>>temp1>>temp2>>temp3;
        student\[i\].ID = temp1;
        student\[i\].De = temp2;
        student\[i\].Cai = temp3;
        student\[i\].Zong = temp2 + temp3;
        if(temp2>=low && temp3>=low){
            if(temp2>=better && temp3>=better){
                first\_level.push\_back(student\[i\]);
                sum++;
            }
            else if(temp2>=better && temp3<better){
                second\_level.push\_back(student\[i\]);
                sum++;
            }
            else if(temp2>=temp3 && temp3<=better && temp2<=better){
                third\_level.push\_back(student\[i\]);
                sum++;
            }
            else{
                forst\_level.push\_back(student\[i\]);
                sum++;
            }
        }
    }
    cout<<sum<<endl;
    sort(first\_level.begin(),first\_level.end(),cmp2);
    sort(second\_level.begin(),second\_level.end(),cmp2);
    sort(third\_level.begin(),third\_level.end(),cmp2);
    sort(forst\_level.begin(),forst\_level.end(),cmp2);
    for(pos = first\_level.begin();pos!=first\_level.end();pos++){
        cout<<(\*pos).ID<<" "<<(\*pos).De<<" "<<(*pos).Cai<<endl;
    }
    for(pos = second\_level.begin();pos!=second\_level.end();pos++){
        cout<<(\*pos).ID<<" "<<(\*pos).De<<" "<<(*pos).Cai<<endl;
    }
    for(pos = third\_level.begin();pos!=third\_level.end();pos++){
        cout<<(\*pos).ID<<" "<<(\*pos).De<<" "<<(*pos).Cai<<endl;
    }
    for(pos = forst\_level.begin();pos!=forst\_level.end();pos++){
        cout<<(\*pos).ID<<" "<<(\*pos).De<<" "<<(*pos).Cai<<endl;
    }
    return 0;
}

主要介绍一下cmp函数：

bool cmp2(mess a,mess b){
    if(a.Zong != b.Zong){
        return a.Zong>b.Zong;
    }
    else{
        if(a.De != b.De){
            return a.De>b.De;
        }
        else{
            return a.ID<b.ID;
        }
    }
}

cmp参数是在sort进行比较时，各个元素之间进行比较所参考的规则因此这里我设置了各种条件来满足题目中给出的规则。 编写好cmp函数只有就可以作为sort函数的一个参数来使用，从而能够按照你设置的规则进行排序。