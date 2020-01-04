---
title: C++之继承派生
url: 1152.html
id: 1152
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-10 22:01:27
tags:
  - C/C++
  - 继承
---

![](http://47.100.4.8/wp-content/uploads/2018/05/510baad315cd40fc90c092cba2d63480.jpg) 类的继承，是新的类从已有的类那里得到已有的特性。从另一个角度上看，从已有的类中产生新类的过程就是类的派生。 原有的类称为基类或父类，产生的新类称为派生类或子类。派生类也可以作为基类派生新的类，这样就形成了类的层次结构。   派生类的定义： class 派生类名称：继承方式 基类名1，继承方式 基类名2，继承方式 基类名3 { 派生类成员声明； } 代码：
```
#include<iostream>

using namespace std;

class Animal{
public:
    Animal(){};
    ~Animal(){};
    int age;
};

class Dog:public Animal
{
public:
    Dog(){};
    ~Dog(){};
    int SetAge(int n);
};

int Dog::SetAge(int n)
{
    age=n;
    cout<<"age="<<age<<endl;
}
int main()
{
    Dog dog;
    int n=10;
    dog.SetAge(n);
    return 0;
}
```
截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-4.png) 一个派生类，可以同时有多个基类，这种情况称为多继承，这时的派生类同时得到多个已有类的特征。 一个派生类只有一个直接基类的情况称为单继承。 ![](http://47.100.4.8/wp-content/uploads/2018/05/2-4.png) 继承方式关键字：public，protected，private分别表示公有继承，保护继承，私有继承。 1.公有继承，使得基类public（公有）和protected（保护）成员的访问属性在派生类中不变，而基类private（私有）成员不可访问 2.私有继承，使用基类public（公有）和protected（保护）成员都以private（私有）成员身份出现在派生类中，而基类private（私有）成员不可访问。 3.保护继承中，基类public（公有）和protected（保护）成员都已protected（保护）成员身份出现在派生类中，而基类private（私有）成员不可访问。   上面的代码就是使用public公有继承。   构造函数： 构造派生类的对象时，就要对基类的成员对象和新增成员对象进行初始化。 派生类构造函数的一般语法形式： 派生类名：：派生类名（参数表）：基类名1 （），基类名2（）…… { 派生类构造函数的其他初始化操作； }   如果对基类初始化时，需要调用基类带有形参的构造函数，派生类就必须声明构造函数。   析构函数： 同样也要调用基类的成员析构函数和该类的析构函数。   代码：
```
#include<iostream>

using namespace std;

class BaseClass
{
public:
    BaseClass()
    {
        cout<<"     BaseClass's message:Create"<<endl;
    }
    ~BaseClass()
    {
        cout<<"     BaseClass's message:Destroy"<<endl;
    }
};

class DerivedClass:public BaseClass
{
public:
    DerivedClass()
    {
        cout<<"     DerivedClass's message:Create"<<endl;
    }
    ~DerivedClass()
    {
        cout<<"     DerivedClass's message:Destroy"<<endl;
    }

};
int main()
{
    cout<<"MessageBox:"<<endl;
    DerivedClass derivedclass;
    return 0;
}
```
  截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/3-3.png) 由截图可以看出继承构造和析构函数的使用：如果DerivedClass继承于基类BaseClass，则在使用DerivedClass类去声明一个对象时，会先创建一个BaseClass类的对象，然后在创建DerivedClass类的对象，上面是构造函数的调用情况，然后是析构函数的调用情况，是先调用DerivedClass的析构函数，然后再调用BaseClass的析构函数。   **在派生类中可以使用基类名：：基类成员来访问基类中的成员。** 访问方式也会在下面使用到   先介绍一下虚基类： 当某类的部分或全部直接基类是从另一个基类派生而来的，这些直接基类中，从上一级基类继承来的成员就拥有相同的名称，派生类的对象的这些同名成员在内存中同时拥有多个拷贝，我们可以使用作用于分辨符来唯一标识并分别访问他们，我们也可以**将直接基类的共同基类设置为虚基类，这时从不同的路径继承过来的该类成员在内存中只拥有一个拷贝**，这样就解决了同名成员的唯一标识问题。   虚基类的声明是在派生类的声明过程中，其语法格式为： class 派生类名：virtual 继承方式 基类名 在多继承情况下，虚基类关键字的作用范围和继承方式关键字相同，只对紧跟其后的基类起作用，声明了虚基类之后，虚基类的成员在进一步的派生中，和派生类一起维护一个内存数据拷贝。   图示： ![](http://47.100.4.8/wp-content/uploads/2018/05/4-3.png) 使用 代码：
```
#include<iostream>
#include<string.h>

using namespace std;

class vehicle{
public:
    vehicle()
    {
        cout<<"     Vehicle's message:Create"<<endl;
    }
    ~vehicle()
    {
        cout<<"     Vehicle's message:Destroy"<<endl;
    }
    int Lunzi;  //轮子数目
    int Price;  //价格

    void SetLunZi(int n)
    {
        Lunzi=n;
    }

    void SetPrice(int n)
    {
        Price = n;
    }
};

class bicycle:virtual public vehicle
{
public:
    bicycle()
    {
        cout<<"     bicycle's message:Create"<<endl;
    }
    ~bicycle()
    {
        cout<<"     bicycle's message:Destroy"<<endl;
    }
    string PinPai;  //品牌
    void SetPinPai(string a)
    {
        PinPai = a;
    }
};

class motorcar:virtual public vehicle
{
public:
    motorcar()
    {
        cout<<"     motorcar's message:Create"<<endl;
    }
    ~motorcar()
    {
        cout<<"     motorcar's message:Destroy"<<endl;
    }
    string PinPai;  //品牌
    void SetPinPai(string a)
    {
        PinPai = a;
    }
};

class motorcycle:public bicycle,public motorcar
{
public:
    motorcycle()
    {
        cout<<"     motorcycle's message:Create"<<endl;
    }
    ~motorcycle()
    {
        cout<<"     motorcycle's message:Destroy"<<endl;
    }
    void SetMessage(string a,int b,int c,int d)
    {
        bicycle::SetPinPai(a);
        vehicle::SetPrice(b);
        vehicle::SetLunZi(c);
        v=d;
    }
    void OutMessage()
    {
        cout<<"     摩托车品牌名称："<<bicycle::PinPai<<endl;
        cout<<"     摩托车价格："<<vehicle::Price<<"元"<<endl;
        cout<<"     摩托车轮子数；"<<vehicle::Lunzi<<"个"<<endl;
        cout<<"     摩托车速度："<<v<<"km/h"<<endl;
    }
private:
    int v;  //速度
};


int main()
{
    cout<<"MessageBox:"<<endl;
    motorcycle mb;
    cout<<"输入摩托车品牌名称：";
    string s1;
    cin>>s1;
    cout<<"输入摩托车价格：";
    int a;
    cin>>a;
    cout<<"输入摩托车轮子数；";
    int b;
    cin>>b;
    cout<<"输入摩托车速度：";
    int c;
    cin>>c;
    mb.SetMessage(s1,a,b,c);
    cout<<"摩托车信息显示："<<endl;
    mb.OutMessage();
    return 0;
}

```
截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/5-1.png)