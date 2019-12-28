---
title: C++之多态性
url: 1201.html
id: 1201
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-17 22:19:52
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 多态性概述： 多态是指同样的消息被不同类型的对象接收时导致不同的行为。消息是指对类的成员函数调用，不同的行为是指不同的实现。 例如：浮点数和整型数，则要先将整形数转换为浮点数，然后在进行运算。   面向对象的多态可以分为4类：重载多态，强制多态，包含多态和参数多态。 对函数的重载都属于重载多态，接下来还会介绍运算符的重载。 强制多态是指将一个变元的类型加以变化，以符合一个函数或者操作的要求，比如类型的强制转换就是强制多态。， 包含多态是类族中定义于不同类中的同名成员函数的多态性为，主要通过虚函数来实现，在后面也会给出例子。 参数多态与类模板相关联。   多态从实现的角度来讲可以划分为两类：编译时的多态和运行时的多态。 前者是在编译的过程中确定了同名操作的具体操作对象，而后者则是在程序运行过程中才动态地确定操作所针对的具体对象。这种确定操作的具体对象的过程就是绑定。 绑定是指计算机程序本身彼此关联的过程。（实质上就是把一条消息和对象的方法相结合的过程）   绑定工作在编译连接阶段完成的情况称为静态绑定。 绑定工作在程序运行阶段完成的情况称为动态绑定。   运算符重载是对已有的运算符赋予多重含义，是同一个运算符作用于不同类型的数据是导致不同的行为。 比如：在string库文件中 就对+等运算进行了重载，这里的+号是进行两个字符串的连接。 重载运算符的规则：

*   c++中的运算符除了少数几个之外，全部可以重载，而且只能重载C++中已经有的运算符。
*   重载之后运算符的优先级和结合性都不会改变
*   运算符重载是针对新类型数据的实际需要，对原有的运算符进行适当的改造。

**给出不能重载的运算符：“.”类关系运算符，“.*”成员指针运算符，“::”作用域分辩符，“？：”三木运算符。**  两种重载运算符的形式：

1.  重载类的非静态成员函数声明的语法形式：

返回类型 operator 运算符（形参表） { 函数体; }

2.  运算符重载为非成员函数的一般语法形式：

返回类型 operator 运算符（形参表） { 函数体; } 貌似两个格式上没差啊！   运算符的重载实质上就是成员函数的重载，重载为成员函数。它可以自由的访问该类中的数据成员。 **需要注意的是：如果是双目运算符，左操作数是对象本身的数据，由this指针指出。右操作数则需要通过运算符重载函数的参数表指出。** 上面需要的主要的内容就在下面例子有了很好的解释。为什么在重载—a时需要使用int参数表。   下面给出一个运算符重载为成员函数的例子： 重载a++ 、++a 、a-- 、--a 运算符： 代码：

#include<iostream>



using namespace std;



class Point{

public:

    Point(int x,int y);

    ~Point(){};

    Point& operator++();  //对a++进行重载

    Point operator++(int i); //对++a 进行重载

    Point& operator--(); //对a--进行重载

    Point operator--(int i);   //对--a进行重载

    void print(); //打印坐标点

private:

    int _x;

    int _y;

};



Point::Point(int x,int y)

{

    _x=x;

    _y=y;

}



Point& Point::operator++()

{

    _x+=1;

    _y+=1;

    return *this;

}



Point Point::operator++(int)

{

    Point temp=*this;

    ++*this;

    return temp;

}



Point& Point::operator--()

{

    _x-=1;

    _y-=1;

    return *this;

}



Point Point::operator--(int)

{

   Point temp = *this;

   --*this;

   return temp;

}



void Point::print()

{

    cout<<\_x<<" "<<\_y<<endl;

}



int main()

{

    int x1,y1;

    cout<<"点point1的x和y坐标:";

    cin>>x1>>y1;

    Point point1(x1,y1);

    cout<<"使用重载的a++之后的坐标：";

    point1++;

    point1.print();

    cout<<"使用重载的++a之后的坐标：";

    ++point1;

    point1.print();

    cout<<"使用重载的a--之后的坐标：";

    point1--;

    point1.print();

    cout<<"使用重载的--a之后的坐标：";

    --point1;

    point1.print();

    return 0;

}

    截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/123123123.png) 虚函数 虚函数是动态绑定的基础。虚函数必须是非静态成员的函数。虚函数经过派生之后，在类族中就可以实现运行程序过中的多态，也就是包含多态。   一般虚函数成员的声明语法是： virtual 函数类型 函数名（形参表）； 注意：虚函数声明只能出现在类定义中的函数原型声明中，而不能在成员函数实现的时候。 即为：在类中要声明是一个虚函数，而不是在类外部实现时。   需要注意的几点：

1.  类之间满足赋值兼容规则
2.  要声明虚函数
3.  由成员函数来调用或者是通过指针、引用来访问虚函数。、

  对于在派生类中虚函数自己的理解： 如果用一个基类来声明一个指针并指向它的派生子类时需要使用new 来动态创建。 并且在使用派生子类的成员函数时，需要在基类中声明该成员函数并且声明为虚函数，这样才可以使用派生子类的成员函数。在下面的例子中也会用到 接下来给出一个例子 代码：

#include<iostream>

#include<Windows.h>



using namespace std;



class vehicle{

public:

    vehicle()

    {

        cout<<"     Vehicle's message:Create"<<endl;

    }

    ~vehicle()

    {

        cout<<"     Vehicle's message:Destroy"<<endl;

    }

    int Lunzi;  //轮子数目

    int Price;  //价格



    void SetLunZi(int n)

    {

        Lunzi=n;

    }



    void SetPrice(int n)

    {

        Price = n;

    }

    void virtual Run(){int i;};

    void virtual Stop(){int i;};

private:

    int v;

};



class bicycle:virtual public vehicle

{

public:

    bicycle()

    {

        cout<<"     bicycle's message:Create"<<endl;

    }

    ~bicycle()

    {

        cout<<"     bicycle's message:Destroy"<<endl;

    }

    string PinPai;  //品牌

    void SetPinPai(string a)

    {

        PinPai = a;

    }

    void Run()

    {

        v=0; //速度初值为0

        cout<<"自行车启动！"<<endl;

        for(int i=0;i<5;i++)  //自行车最大速度为30km/s

        {

            v=i+1;

            Sleep(300);

            cout<<"当前自行车的速度为："<<v<<"km/s"<<endl;

        }

    }

    void Stop()

    {

        cout<<"开始刹车！"<<endl;

        Sleep(500);

        cout<<"自行车停止速度变为："<<v<<"km/s"<<endl;

        v=0;



    }

private:

    int v;

};



class motorcar:virtual public vehicle

{

public:

    motorcar()

    {

        cout<<"     motorcar's message:Create"<<endl;

    }

    ~motorcar()

    {

        cout<<"     motorcar's message:Destroy"<<endl;

    }

    string PinPai;  //品牌

    void SetPinPai(string a)

    {

        PinPai = a;

    }

    void Run()

    {

        v=0; //速度初值为0

        cout<<"汽车启动！"<<endl;

        for(int i=0;i<10;i++)  //自行车最大速度为30km/s

        {

            v=i+1;

            Sleep(200);

            cout<<"当汽车的速度为："<<v<<"km/s"<<endl;

        }

    }

    void Stop()

    {

        cout<<"开始刹车！"<<endl;

        Sleep(400);

        cout<<"汽车完全停止,速度变为："<<v<<"km/s"<<endl;

        v=0;



    }

private:

    int v;

};



class motorcycle:public bicycle,public motorcar

{

public:

    motorcycle()

    {

        cout<<"     motorcycle's message:Create"<<endl;

    }

    ~motorcycle()

    {

        cout<<"     motorcycle's message:Destroy"<<endl;

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

        cout<<"     摩托车品牌名称："<<bicycle::PinPai<<endl;

        cout<<"     摩托车价格："<<vehicle::Price<<"元"<<endl;

        cout<<"     摩托车轮子数；"<<vehicle::Lunzi<<"个"<<endl;

        cout<<"     摩托车速度："<<v<<"km/h"<<endl;

    }

    void Run()

    {

        v=0; //速度初值为0

        cout<<"摩托车启动！"<<endl;

        for(int i=0;i<8;i++)  //摩托车最大速度为100km/s

        {

            v=i+1;

            Sleep(250);

            cout<<"当前摩托车的速度为："<<v<<"km/s"<<endl;

        }

    }

    void Stop()

    {

        cout<<"开始刹车！"<<endl;

        Sleep(400);

        cout<<"摩托车停止速度变为："<<v<<"km/s"<<endl;

        v=0;



    }

private:

    int v;  //速度

};



int main()

{

    vehicle *bike1 =new motorcycle();

    vehicle *bike2 =new bicycle();

    vehicle *bike3 =new motorcar();

    bike1->Run();

    cout<<endl;

    bike1->Stop();

    cout<<endl<<endl;

    bike2->Run();

    cout<<endl;

    bike2->Stop();

    cout<<endl<<endl;

    bike3->Run();

    cout<<endl;

    bike3->Stop();

    return 0;

}

    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/312312313.png) 通过上面的例子可以看出 **如果在派生类中没有显示给出声明的话，系统则遵循下面规则进行判断派生类的一个成员函数是不是虚函数：**

1.  **该函数是否与基类的虚函数有相同的名称。**
2.  **该函数是否与基类的虚函数有相同的参数个数，以相同的对应参数类型。**
3.  **该函数是否与基类的虚函数有相同的返回值或者满足赋值兼容规则的指针、引用型的返回值。**

**如果均满足就会被认定为虚函数。这个时候派生类的成员函数会覆盖掉基类的虚函数！** 同样如果有多个派生类均会覆盖。