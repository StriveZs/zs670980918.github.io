---
title: Pat_1015（乙级）
url: 1649.html
id: 1649
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:14:02
tags:
  - pat
---

1015 德才论 （25 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805307551629312

宋代史学家司马光在《资治通鉴》中有一段著名的“德才论”：“是故才德全尽谓之圣人，才德兼亡谓之愚人，德胜才谓之君子，才胜德谓之小人。凡取人之术，苟不得圣人，君子而与之，与其得小人，不若得愚人。” 现给出一批考生的德才分数，请根据司马光的理论给出录取排名。

### 输入格式：

输入第一行给出 3 个正整数，分别为：N（≤10​5​​），即考生总数；L（≥60），为录取最低分数线，即德分和才分均不低于 L 的考生才有资格被考虑录取；H（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于 H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线 L 的考生也按总分排序，但排在第三类考生之后。 随后 N 行，每行给出一位考生的信息，包括：`准考证号 德分 才分`，其中`准考证号`为 8 位整数，德才分为区间 \[0, 100\] 内的整数。数字间以空格分隔。

### 输出格式：

输出第一行首先给出达到最低分数线的考生人数 M，随后 M 行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。

### 输入样例：

    14 60 80
    10000001 64 90
    10000002 90 60
    10000011 85 80
    10000003 85 80
    10000004 80 85
    10000005 82 77
    10000006 83 76
    10000007 90 78
    10000008 75 79
    10000009 59 90
    10000010 88 45
    10000012 80 100
    10000013 90 99
    10000014 66 60
    

### 输出样例：

    12
    10000013 90 99
    10000012 80 100
    10000003 85 80
    10000011 85 80
    10000004 80 85
    10000007 90 78
    10000006 83 76
    10000005 82 77
    10000002 90 60
    10000014 66 60
    10000008 75 79
    10000001 64 90

代码：
```
#include<iostream>
#include<algorithm>
#include<vector>

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
    vector<mess> first_level;
    vector<mess> second_level;
    vector<mess> third_level;
    vector<mess> forst_level;
    vector<mess>::iterator pos;
    for(int i=0;i<num;i++){
        cin>>temp1>>temp2>>temp3;
        student\[i\].ID = temp1;
        student\[i\].De = temp2;
        student\[i\].Cai = temp3;
        student\[i\].Zong = temp2 + temp3;
        if(student\[i\].De>=low && student\[i\].Cai>=low){
            if(student\[i\].De>=better && student\[i\].Cai>=better){
                first\_level.push\_back(student\[i\]);
                sum++;
            }
            else if(student\[i\].De>=better && student\[i\].Cai<better){
                second\_level.push\_back(student\[i\]);
                sum++;
            }
            else if(student\[i\].De>=student\[i\].Cai && student\[i\].Cai<=better && student\[i\].De<=better){
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

上面代码由于使用的算法不够好，导致两个测试点运行超时 下面改正过得：

#include<vector>  
#include<cstdio>  
#include<algorithm>  
using namespace std;  
  
struct student  
{  
    int kaohao;  
    int defen;  
    int caifen;  
    int zongfen;  
};  
  
bool compare(student a,student b) //比较a在b前则返回true,表示a在b前面  
{  
    if(a.zongfen>b.zongfen)  
        return true;  
    else if(a.zongfen == b.zongfen)  
    {  
        if(a.defen>b.defen)  
            return true;  
        else if(a.defen==b.defen)  
        {  
            if(a.kaohao<b.kaohao)  
                return true;  
        }  
    }  
    return false;  
}  
  
int main()  
{  
    vector<student> v1,v2,v3,v4;//表示四类考生  
    student stu;//学生信息临时保存  
    int count=0;//达标的学生总数  
    int N,L,H;  
  
    //cin>>N>>L>>H;  
    scanf("%d %d %d",&N,&L,&H);    
    int K,D,C;  
    while(N--)  
    {  
        //cin>>K>>D>>C;  
        scanf("%d%d%d",&K,&D,&C);    
        stu.kaohao = K;  
        stu.defen = D;  
        stu.caifen = C;  
        stu.zongfen = D+C;  
        if(D>=L && C>=L)  
        {  
            count++;  
            if(D>=H && C>=H)  
                v1.push_back(stu);    
            else if(D>=H && C<H )  
                v2.push_back(stu);  
            else if(D<H && C<H  && D>=C)  
                v3.push_back(stu);  
            else   
                v4.push_back(stu);  
        }  
      
    }  
    printf("%d\\n",count);  
    sort(v1.begin(),v1.end(),compare);  
    sort(v2.begin(),v2.end(),compare);  
    sort(v3.begin(),v3.end(),compare);  
    sort(v4.begin(),v4.end(),compare);  
  
    vector<student>::iterator itr;  
    for(itr=v1.begin();itr!=v1.end();itr++)  
        printf("%d %d %d\\n",itr->kaohao,itr->defen,itr->caifen);  
    for(itr=v2.begin();itr!=v2.end();itr++)  
        printf("%d %d %d\\n",itr->kaohao,itr->defen,itr->caifen);  
    for(itr=v3.begin();itr!=v3.end();itr++)  
        printf("%d %d %d\\n",itr->kaohao,itr->defen,itr->caifen);  
    for(itr=v4.begin();itr!=v4.end();itr++)  
        printf("%d %d %d\\n",itr->kaohao,itr->defen,itr->caifen);  
  
    system("pause");  
    return 0;  
}
```