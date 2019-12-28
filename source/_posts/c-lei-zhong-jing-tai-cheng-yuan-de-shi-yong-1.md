---
title: C++类中静态成员的使用
url: 1259.html
id: 1259
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-25 11:48:10
tags:
---

总结一下C++中类静态成员以及成员函数的使用： 先说一下什么是静态成员，静态成员就是即使在重新声明一个对象时，类中的静态成员不会改变（比如下面代码中的ClientNum即使在声明一个新的对象时，没有发生改变二十继续递增）。ps：个人理解 我认为还是给出一个例子来说明是最好的 代码：

#include<iostream>



using namespace std;



class CLIENT

{

public:

    CLIENT()

    {

        ClientNum++;

    }

    virtual ~CLIENT(){};

    static void ChangeServerName(char new_name)  //改变服务器名称

    {

        CLIENT::ServerName=new_name;

    }

    virtual void print();

private:

    static int ClientNum;  //客户数量计数器

    static char ServerName;  //保存服务器名称



};



int CLIENT::ClientNum=0;

char CLIENT::ServerName='\\0';



void CLIENT::print()

{

    cout<<"  当前服务器名称为："<<CLIENT::ServerName<<endl;;

    cout<<"  当前用户数量为："<<CLIENT::ClientNum<<endl;

}

int main()

{

    cout<<"第一个客户到达："<<endl;

    CLIENT client1;

    CLIENT::ChangeServerName('A');

    client1.print();

    cout<<"第二个用户到达："<<endl;

    CLIENT client2;

    client1.print();

    cout<<"第三个用户到达并将服务器的名称修改为B:"<<endl;

    CLIENT client3;

    CLIENT::ChangeServerName('B');

    client1.print();

    return 0;

}

    结果为： ![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180525114719.png) 接下来对上面的代码进行总结： 静态成员函数： 首先需要注意的是在声明静态成员的类中所有非静态成员函数都需要以virtual开头（虚函数） 格式为：virtual 函数类型 函数名（参数表） {函数体} 然后是静态成员函数的声明，格式为 static 函数类型 函数名（参数表）{函数体} 这里貌似只能在类中对静态成员函数进行声明和定义，在外部定义貌似是需要使用到inline（内联函数）。 在使用静态成员函数时的格式为：类名：：函数名， 而不是通过对象名+点号进行引用。   接下来是静态成员的使用： 声明方面只需要在普通声明之前加上static即可，在使用方面的 格式其实和静态函数的使用相似为 类名：：成员名。对了还有一点需要的注意的是在使用静态成员时需要事先在所有函数外部给成员变量赋初值。格式为： 变量类型 类名：：成员名 = 初值。 这里我还稍微修改了一点内容，由于上面的代码没有在类中声明普通的成员，所以我起初感觉可能声明普通成员时需要特殊的格式，然而在经过我测试之后得到的结果是声明普通的成员变量时，不需要添加任何其他的关键词，正常使用即可。