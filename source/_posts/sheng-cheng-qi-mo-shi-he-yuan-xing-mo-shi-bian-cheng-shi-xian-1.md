---
title: 生成器模式和原型模式编程实现
url: 1832.html
id: 1832
categories:
  - C&amp;C++
  - 文章页
  - 设计模式
date: 2019-05-06 12:36:54
tags:
  - generator pattern
  - prototype pattern
---

1、生成器模式的原理：

*   Builder

为创建一个Product对象的各个部件指定抽象接口

*   ConcreteBuilder

实现Builder的接口以构造和装配该产品的各个部件 定义并明确它所创建的表示 提供一个检索产品的接口

*   Director

构造一个使用Builder接口的对象

*   Product

表示被构造的复杂对象。ConcreteBuilder创建该产品的内部表示并定义它的装配过程。 包含定义组成部件的类，包括将这些部件装配成最终产品的接口 **结构图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/1.png) **2、原型模式原理：**

*   Prototype

声明一个克隆自身的接口

*   ConcretePrototype

实现一个克隆自身的操作

*   Client

让一个原型克隆自身从而创建一个新的对象 **结构图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/2.png) **题目要求：** 使用生成器模式模拟实现IBM电脑的生产，其中IBM电脑的主要结构用如下表示： class IBM{   string monitor=”IBM的显示器”;   string keyboard=”IBM的键盘”;   string mouse=”IBM的鼠标”;   Motherboard* MB;   void display(); } 其中MB是一个主板类，其主要结构如下： class Motherboard{ string CPU; string RAM; } 即主板包含CPU和RAM。display是一个打印各个组件的函数，主要用于检查是否生产正确。 建造顺序为先生产主板，再依次生产显示器、键盘和鼠标。 使用生成器模式生产出第一台IBM电脑后，利用原型模式，将该电脑再复制两台。 **UML类图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/3.jpg) **代码：**
```
#include<iostream>
#include<string.h>

using namespace std;

//Product
//主板
class Motherboard{
public:
    Motherboard(){}
    string CPU;
    string RAM;
    void set_CPU(string CPU){
      this->CPU = CPU;
    }
    void set_RAM(string RAM){
      this->RAM = RAM;
    }
    void display(){
        cout<<"Elements of motherboards!"<<endl;
        cout<<"CPU:"<<CPU<<endl;
        cout<<"RAM:"<<RAM<<endl;
    }
    Motherboard* Clone(){
        return new Motherboard(*this);
    }
private:
    Motherboard(Motherboard* tt){
        tt->CPU = CPU;
        tt->RAM = RAM;
    }
};
//IBM
class IBM{
public:
  IBM(){
      MB = new Motherboard();
  }
  Motherboard* MB;
  string monitor;
  string keyboard;
  string mouse;
  void set_monitor(string monitor){
      this->monitor = monitor;
  }
  void set_keyboard(string keyboard){
      this->keyboard = keyboard;
  }
  void set_mouse(string mouse){
      this->mouse = mouse;
  }
  void display(){
      MB->display();
      cout<<"IBM's monitor:"<<monitor<<endl;
      cout<<"IBM's keyboard:"<<keyboard<<endl;
      cout<<"IBM's mouse:"<<mouse<<endl;
      cout<<"IBM has produced!"<<endl;
  };
  IBM* Clone(){
      IBM* obj = new IBM();
      obj->MB = MB->Clone();
      obj->monitor = monitor;
      obj->keyboard = keyboard;
      obj->mouse = mouse;
      return obj;
  }
};

//Builder
class IBM_Builder{
public:
    virtual void BuildPart_Motherboard()=0;
    virtual void BuildPart_monitor()=0;
    virtual void BuildPart_keyboard()=0;
    virtual void BuildPart_mouse()=0;
    virtual IBM* GetComputer()=0;
};

//ConcreteBuilder
class IBM\_ConcreteBuilder:public IBM\_Builder{
public:
    void BuildPart_Motherboard(){
        computer->MB->set_CPU("i9-9900K");
        computer->MB->set_RAM("Kingston 3800MHZ");
    }
    void BuildPart_monitor(){
        computer->set_monitor("SamSung");
    }
    void BuildPart_keyboard(){
        computer->set_keyboard("cherry");
    }
    void BuildPart_mouse(){
        computer->set_mouse("G903");
    }
    IBM* GetComputer(){
        return computer;
    }
private:
    IBM* computer = new IBM();
};

//Director
class IBM_Director{
public:
    void Construct(IBM_Builder *builder){
        builder->BuildPart_Motherboard();
        builder->BuildPart_monitor();
        builder->BuildPart_keyboard();
        builder->BuildPart_mouse();
    }
};

int main(){
    IBM\_ConcreteBuilder* t1 = new IBM\_ConcreteBuilder();
    IBM\_Director* t2 = new IBM\_Director();
    t2->Construct(t1);
    IBM *p1 = t1->GetComputer();
    p1->display();
    IBM *p2 = p1->Clone();
    p2->display();
    IBM *p3 = p1->Clone();
    p3->display();
    p3->set_monitor("1111");
    p3->display();
    p1->display();
    return 0;
}
```
**结果：** ![](http://47.100.4.8/wp-content/uploads/2019/05/4.png)