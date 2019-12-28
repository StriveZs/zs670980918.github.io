---
title: 装饰模式编程实现
url: 1844.html
id: 1844
categories:
  - C&amp;C++
  - 文章页
  - 设计模式
date: 2019-05-13 15:04:12
tags:
---

**装饰模式**

**实验原理：**

*   动态地给一个对象添加一些额外的职责。
*   就增加功能来说，装饰模式比生成子类更为灵活。

**装饰模式的适用性：**

*   在不影响其他对象的情况下，以动态、透明的方式给单个对象添加职责。
*   处理那些可以撤销的职责。
*   当不能采用生成子类的方法进行扩充时。
*   可能有大量独立的扩展，为支持每一种组合将产生大量的子类，使得子类数目呈爆炸性增长。
*   类定义被隐藏，或类定义不能用于生成子类。

**装饰模式的结构：** ![](http://47.100.4.8/wp-content/uploads/2019/05/11.png) **例题：** 给定两种初始的汽车类，例如丰田和沃尔沃，利用装饰模式分别给它们添加新的功能，其中丰田可以导航和自动驾驶，沃尔沃可以导航和语音控制。 **代码：**

#include<iostream>
using namespace std;
class Car{
public:
    virtual void Operation()=0;
};
//Decorator
class Decorator:public Car{
protected:
    Car* car;
public:
    void SetCar(Car* car){
        this->car = car;
    }
    void Operation(){
        if(car != NULL){
            car->Operation();
        }
    }
};
//导航
class ConcreteFunction1:public Decorator{
public:
    void Operation(){
        Decorator::Operation();
        cout<<"Navigation"<<endl;
    }
};
//自动驾驶
class ConcreteFunction2:public Decorator{
public:
    void Operation(){
        Decorator::Operation();
        cout<<"Autopilot"<<endl;
    }
};
//语音控制
class ConcreteFunction3:public Decorator{
public:
    void Operation(){
        Decorator::Operation();
        cout<<"Voice control"<<endl;
    }
};
//丰田
class Toyota:public Car{
public:
    void Operation(){
        cout<<"Toyota:"<<endl;
    }
};
//沃尔沃
class Volvo:public Car{
public:
    void Operation(){
        cout<<"Volvo:"<<endl;
    }
};
int main(){
    Toyota* toyota = new Toyota();
    ConcreteFunction1* concreteFunction1 = new ConcreteFunction1();
    ConcreteFunction2* concreteFunction2 = new ConcreteFunction2();
    concreteFunction1->SetCar(toyota);
    concreteFunction2->SetCar(concreteFunction1);
    concreteFunction2->Operation();
    Volvo* volvo = new Volvo();
    ConcreteFunction1* concreteFunction3 = new ConcreteFunction1();
    ConcreteFunction3* concreteFunction4 = new ConcreteFunction3();
    concreteFunction3->SetCar(volvo);
    concreteFunction4->SetCar(concreteFunction3);
    concreteFunction4->Operation();
    return 0;
}

**UML类图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/2-2.png) **结果：** ![](http://47.100.4.8/wp-content/uploads/2019/05/3-1.png)