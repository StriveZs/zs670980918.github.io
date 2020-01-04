---
title: 适配器模式编程实现
url: 1838.html
id: 1838
categories:
  - C&amp;C++
  - 文章页
  - 设计模式
date: 2019-05-08 19:02:27
tags:
  - adaptor pattern
---

适配器模式

**适配器模式的结构：**

*   客户端使用的Target类需要使用一个已经存在的接口Adaptee类，可以用两种方法实现：
*   构造Adapter类继承Target类，并实现Adaptee接口（适配器模式的类版本）
*   将一个Adaptee实例作为Adapter的组成部分（适配器模式的对象版本）

**类版本结构：** ![](http://47.100.4.8/wp-content/uploads/2019/05/1-1.png) **对象版本:** ![](http://47.100.4.8/wp-content/uploads/2019/05/2-1.png) **适配器模式的参与者：**

*   Target

定义Client使用的与特定领域相关的接口

*   Client

与符合Target接口的对象协同

*   Adaptee

定义一个已经存在的接口，这个接口需要适配

*   Adapter

对Adaptee的接口与Target接口进行适配 **使用例题：** 分别利用类版本和对象版本的适配器模式模拟实现ps2接口和usb接口的转换。 我们手中有个ps2插头的设备，但是主机上只有usb插头的接口，实现一个适配器将ps2接口转换为usb接口。其中，ps2接口表示为： class Ps2{ virtual void isPs2(); } Usb接口表示为： class Usb{ Virtual void isusb(); }。 **对象版本的代码：**
```
#include<iostream>

using namespace std;
//类版本
//Adaptee
//定义一个已经存在的接口，这个接口需要适配
class Ps2{
public:
    void isPs2(){
        cout<<"Ps2"<<endl;
    };
};
//Target
class Usb{
public:
    virtual void isUsb()=0;
};
//对Adaptee的接口与Target接口进行适配
class Adapter:public Usb{
public:
    void isUsb(){
        ps2->isPs2();
    }
private:
    Ps2* ps2 = new Ps2();
};

int main(){
    Usb* usb = new Adapter();
    usb->isUsb();
    return 0;
}

**对应的UML类图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/3.png) **类版本的代码：**

#include<iostream>

using namespace std;
//类版本
//Adaptee
//定义一个已经存在的接口，这个接口需要适配
class Ps2{
public:
    void isPs2(){
        cout<<"Ps2"<<endl;
    };
};
//Target
class Usb{
public:
    virtual void isUsb()=0;
};
//对Adaptee的接口与Target接口进行适配
class Adapter:public Usb,private Ps2{
    void isUsb(){
        isPs2();
    }
};

int main(){
    Usb* usb = new Adapter();
    usb->isUsb();
    return 0;
}
```
**对应的UML类图：** ![](http://47.100.4.8/wp-content/uploads/2019/05/4-1.png)