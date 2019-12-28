---
title: Chomsky文法类型判断
url: 1618.html
id: 1618
categories:
  - C&amp;C++
  - 文章页
  - 编译原理
date: 2019-02-14 13:40:46
tags:
---

四种文法类型

**1****．0型文法（短语文法）** 如果对于某文法G，P中的每个规则具有下列形式：   u:: = v 其中u∈V＋，v∈V*，则称该文法G为0型文法或短语文法，简写为PSG。 0型文法或短语结构文法的相应语言称为0型语言或短语结构语言L0。这种文法由于没有其他任何限制，因此0型文法也称为无限制文法，其相应的语言称为无限制性语言。任何0型语言都是递归可枚举的，故0型语言又称递归可枚举集。这种语言可由图灵机（Turning）来识别。   **2****．1型文法（上下文有关文法）** 如果对于某文法G，P中的每个规则具有下列形式：   xUy:: = xuy 其中U∈VN；u∈V＋；x，y∈V*，则称该文法G为1型文法或上下文有关文法，也称上下文敏感文法，简写为CSG。 1型文法的规则左部的U和右部的u具有相同的上文x和下文y，利用该规则进行推导时，要用u替换U，必须在前面有x和后面有y的情况下才能进行，显示了上下文有关的特性。 1型文法所确定的语言为1型语言L1，1型语言可由线性有界自动机来识别。   **3****．2型文法（上下文无关文法）** 如果对于某文法G，P中的每个规则具有下列形式：   U :: = u 其中U∈VN；u∈V＋，则称该文法G为2型文法或上下文无关文法，简写为CFG。 按照这条规则，对于上下文无关文法，利用该规则进行推导时，无需考虑非终结符U所在的上下文，总能用u替换U，或者将u归约为U，显示了上下文无关的特点。 2型文法所确定的语言为2型语言L2，2型语言可由非确定的下推自动机来识别。 一般定义程序设计语言的文法是上下文无关的。如C语言便是如此。因此，上下文无关文法及相应语言引起了人们较大的兴趣与重视。   **4****．3型文法（正则文法，线性文法）** 如果对于某文法G，P中的每个规则具有下列形式：   U :: = T  或  U :: = WT 其中T∈VT；U,W∈VN，则称该文法G为左线性文法。 如果对于某文法G，P中的每个规则具有下列形式：   U :: = T  或  U :: = TW 其中T∈VT；U, W∈VN，则称该文法G为右线性文法。 左线性文法和右线性文法通称为3型文法或正则文法，有时又称为有穷状态文法，简写为RG。 按照定义，对于正则文法应用规则时，单个非终结符号只能被替换为单个终结符号，或被替换为单个非终结符号加上单个终结符号，或者被替换为单个终结符号加上单个非终结符号。 3型文法所确定的语言为3型语言L3，3型语言可由确定的有限状态自动机来识别。 在常见的程序设计语言中，多数与词法有关的文法属于3型文法。 可以看出，上述4类文法，从0型到3型，产生式限制越来越强，其后一类都是前一类的子集，而描述语言的功能越来越弱，四类文法及其表示的语言之间的关系可表示为： 0型1型2型3型；即L0 L1 L2 L3 代码：

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

使用： ![](http://47.100.4.8/wp-content/uploads/2019/02/QQ图片20190214133918.png) 提供一些测试用例：

*   0型文法数据

ABC->ab SABC->sAb ScDE->bc

*   1型文法数据

AB->ab SA->Sa SB->Sb S->Sac

*   2型文法数据

S->SABc S->a A->ab B->de

*   3型文法数据

右线型： A->aB A->a 左线型： A->Ba A->a