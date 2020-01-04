---
title: C++实现Chomsky文法类型判断
url: 1570.html
id: 1570
categories:
  - C&amp;C++
  - 文章页
  - 编译原理
date: 2018-11-05 20:00:41
tags:
  - C/C++
  - Chomsky
  - 文法类型判断
  - grammar
---

![](http://47.100.4.8/wp-content/uploads/2018/11/123123.png) **最近在学编译原理，实验课上也让写了文法类型的判断，这里是我自己写的一个Chomsky文法类型的判断** 主要核心思想： 1.先判断是否属于0型文法（判断依据：α->β 其中α和β属于（非终结字符∪终结字符）的闭包的话，并且α至少含有一个非终结字符） 2.如果不是0型文法则结束，如果是0型文法的话，判断是否为1型文法（α的长度≤β的长度） 3.如果不是1型文法则结束，如果是1型文法的话，判断是否为2型文法（α是一个非终结字符，β同上的） 4.如果不是2型文法则结束，如果是2型文法的话，判断是否为3型文法（每个产生式的形式都是A->aB或者A->a） 5.还添加了右线型3型文法的判断和左线型3型文法的判断   **系统流程图：** ![](http://47.100.4.8/wp-content/uploads/2018/11/312312.png) **代码：**
```
#include<iostream>
#include<string>

using namespace std;

struct Gramer{

    string sentence;
    int sl;  //->左侧的字符个数
    int sr;  //->右侧的字符个数
};

Gramer gramer\[20\];
int gramerFlag\[20\]\[5\] = {0}; //用来保存每个产生式的文法类型  第五个值用来标志如果是第3型文法那么他是右线型还是左线型
int sumnum = 0; //输入的产生式总数
string Vn = "";
string Vt = "";

//数据输入和处理
void StartAndHandle(){
    int i = 0;
    int over;
    cout<<"请输入规则："<<endl<<endl;
    while(true){
        sumnum = i+1;
        over = 0; //用来处理如何不是该文法时直接结束本次循环
        cin>>gramer\[i\].sentence;
        if(gramer\[i\].sentence == "$"){   //输入$符号表示规则输入结束
            break;
        }
        int length = gramer\[i\].sentence.length();
        int numl = gramer\[i\].sentence.find('-');
        int numr = gramer\[i\].sentence.find('>');
        gramer\[i\].sl = numl;
        gramer\[i\].sr = length - numr - 1;
        //判断是否为0型文法
        if(gramer\[i\].sl !=0 && gramer\[i\].sr != 0){
            //判断是否有左部非终结字符
            over = 1;
            for (int j = 0;j < gramer\[i\].sl;j++){
                if(gramer\[i\].sentence\[j\] >= 'A' && gramer\[i\].sentence\[j\] <= 'Z'){
                    over = 0;
                    break;
                }
            }
            if(over == 0){
                gramerFlag\[i\]\[0\] = 1;
            }
        }
        else{
            over = 1;
        }
        //是否结束判断
        if(over == 1){
            i++;
            continue;
        }
        else{
            //判断是否为1型文法
            if((gramer\[i\].sl <= gramer\[i\].sr)&&(length != 0)){
                gramerFlag\[i\]\[1\] = 1;
            }
            else{
                over = 1;
            }
            //是否结束判断
            if(over == 1){
                i++;
                continue;
            }
            else{
                //判断是否为2型文法
                if(gramer\[i\].sl == 1){
                    if(gramer\[i\].sentence\[0\] < 'A' || gramer\[i\].sentence\[0\] > 'Z'){
                        over = 1;
                    }
                    if(over == 0){
                        gramerFlag\[i\]\[2\] = 1;
                    }
                }
                else{
                    over = 1;
                }
                //判断是否结束
                if(over == 1){
                    i++;
                    continue;
                }
                else{
                    //判断是否为3型文法
                    if(gramer\[i\].sr == 2){
                        if(gramer\[i\].sentence\[numr+1\] >= 'a' && gramer\[i\].sentence\[numr+1\] <= 'z'){
                            if(gramer\[i\].sentence\[numr+2\] >= 'A' && gramer\[i\].sentence\[numr+2\] <= 'Z'){
                                gramerFlag\[i\]\[3\] = 1;
                                gramerFlag\[i\]\[4\] = 1; //1表示右线型
                            }
                        }
                        if(gramer\[i\].sentence\[numr+1\] >= 'A' && gramer\[i\].sentence\[numr+1\] <= 'Z'){
                            if(gramer\[i\].sentence\[numr+2\] >= 'a' && gramer\[i\].sentence\[numr+2\] <= 'z'){
                                gramerFlag\[i\]\[3\] = 1;
                                gramerFlag\[i\]\[4\] = 2; //1表示左线型
                            }
                        }
                    }
                    if(gramer\[i\].sr == 1)
                        if(gramer\[i\].sentence\[numr+1\] >= 'a' && gramer\[i\].sentence\[numr+1\] <= 'z'){
                                gramerFlag\[i\]\[3\] = 1;
                                gramerFlag\[i\]\[4\] = 0; //表示A->a形式的文法
                }
            }
        }
       i++;
        }
    }
}

//求数组中值的最大值
int getMaxNum(int a\[\],int num){
    int maxs = 0;
    for(int i=0;i<num;i++){
        if(a\[i\]>maxs){
            maxs = a\[i\];
        }
    }
    return maxs;
}

//求数组中值的最小值
int getMinNum(int a\[\],int num){
    int mins = 10;
    for(int i=0;i<num;i++){
        if(a\[i\] < mins){
            mins = a\[i\];
        }
    }
    return mins;
}

//打印一维函数
void Printer1(int a\[\],int num){
    for(int i=0;i<num;i++){
        cout<<a\[i\]<<" ";
    }
    cout<<endl;
}

//打印规则函数
void Printer2(Gramer a\[\],int num1){
    for(int i=0;i<num1;i++){
            cout<<"               "<<a\[i\].sentence<<endl;
    }
}

//规则文法类型的判断
void RuleJudge(){
    int num = sumnum -1; //实际产生式总数
    int flag = 0; //文法类型标志
    int minFlag = 0;
    int sumFlag\[num\]={0};
    for(int i = 0;i < num;i++){
        for(int j = 0;j < 5;j++){
            sumFlag\[i\] = sumFlag\[i\] + gramerFlag\[i\]\[j\];
        }
    }
    int summin = getMinNum(sumFlag,num) - 1;
    int summax = getMaxNum(sumFlag,num) - 1;
    //三型文法特殊处理
    if(summin == summax){
        if(summin == 3){
            cout<<"该规则是3型文法，既是左线型又是右线型"<<endl;
        }
        if(summin == 4){
            cout<<"该规则是3型右线型文法"<<endl;
        }

        if(summin == 5){
            cout<<"该规则是3型左线型文法"<<endl;
        }

        if(summin == 2){
            cout<<"该规则是2型文法"<<endl;
        }

        if(summin == 1){
            cout<<"该规则是1型文法"<<endl;
        }

        if(summin == 0){
            cout<<"该规则是0型文法"<<endl;
        }

    }
    if(summin < summax){
        if(summin == 3 && summax ==4){
            cout<<"该规则是3型右线型文法"<<endl;
        }
        if(summin == 3 && summax ==5){
            cout<<"该规则是3型左线型文法"<<endl;
        }
        if(summin == 4 && summax ==5){
            cout<<"该规则是3型文法,既不是左线型又是右线型"<<endl;
        }
        else{
            if(summin == 0 )
                cout<<"该规则是0型文法"<<endl;
            if(summin == 1)
                cout<<"该规则是1型文法"<<endl;
            if(summin == 2)
                cout<<"该规则是2型文法"<<endl;
        }

    }
    if(summax < 0){
        cout<<"不属于任何文法！"<<endl;
    }
}
int num1 = 0; //Vn长度
int num2 = 0; //Vt长度
//辅助查找函数
int Search1(char a,int num){
    int flag = 1;
    for (int i=0;i<num;i++)
    if(Vn\[i\] == a){
        flag = 0;
        break;
    }
    return flag;
}
int Search2(char a,int num){
    int flag = 1;
    for (int i=0;i<num;i++)
    if(Vt\[i\] == a){
        flag = 0;
        break;
    }
    return flag;
}
//统计非终结字符和终结字符

void TongJi(){
    int num = sumnum -1;
    for(int i=0;i<sumnum;i++){
        int length = gramer\[i\].sentence.length();
        for(int j=0;j<length;j++){
            if(gramer\[i\].sentence\[j\]>='A' && gramer\[i\].sentence\[j\]<='Z'){
                if(Search1(gramer\[i\].sentence\[j\],num1) == 1 && gramer\[i\].sentence\[j\] != '-' && gramer\[i\].sentence\[j\] != '>'){
                    Vn\[num1\] = gramer\[i\].sentence\[j\];
                    num1++;
                }
            }
            if(gramer\[i\].sentence\[j\]>='a' && gramer\[i\].sentence\[j\]<='z'){
                if(Search2(gramer\[i\].sentence\[j\],num2) == 1 && gramer\[i\].sentence\[j\] != '-' && gramer\[i\].sentence\[j\] != '>'){
                    Vt\[num2\] = gramer\[i\].sentence\[j\];
                    num2++;
                }
            }
        }
    }
}


int main(){
    StartAndHandle();
    cout<<endl<<"打印输入的规则:"<<endl;
    Printer2(gramer,sumnum-1);
    cout<<endl;
    RuleJudge();
    TongJi();
    cout<<endl;
    cout<<"非终结字符集合："<<endl;
    cout<<"              Vn= ";
    for(int i =0;i<num1;i++)
        cout<<Vn\[i\]<<" ";
    cout<<endl;
    cout<<endl;
    cout<<"终结字符集合："<<endl;
    cout<<"            Vt= ";
    for(int i =0;i<num2;i++)
        cout<<Vt\[i\]<<" ";
    cout<<endl;
    return 0;
}
```
**结果：** ![](http://47.100.4.8/wp-content/uploads/2018/11/13433213123.png) ![](http://47.100.4.8/wp-content/uploads/2018/11/123123123123.png)