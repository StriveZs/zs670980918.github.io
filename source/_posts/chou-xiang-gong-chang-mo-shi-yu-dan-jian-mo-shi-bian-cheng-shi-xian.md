---
title: 抽象工厂模式与单件模式编程实现
url: 1821.html
id: 1821
categories:
  - C&amp;C++
  - 文章页
  - 设计模式
date: 2019-04-14 13:20:58
tags:
---

一、抽象工厂原理            AbstractFactory            声明一个创建抽象产品对象的操作接口。            ConcreteFactory            实现创建具体产品对象的操作。            AbstractProduct            为一类产品对象声明一个接口。            ConcreteProduct            定义一个将被相应的具体工厂创建的产品对象。            实现AbstractProduct接口。            Client            仅使用由AbstractFactory和AbstractProduct类声明的接口 抽象工厂中的协作：            通常在运行时刻创建一个ConcreteFactory类的实例。这一具体的工厂创建具有特定实现的产品对象。为创建不同的产品对象，客户应使用不同的具体工厂。            AbstractFactory将产品对象的创建延迟到它的ConcreteFactory子类。 抽象工厂中的类图： ![](http://47.100.4.8/wp-content/uploads/2019/04/1.png) 二、单件模式原理            Prototype            声明一个克隆自身的接口            ConcretePrototype            实现一个克隆自身的操作            Client            让一个原型克隆自身从而创建一个新的对象 单件模式的结构：            将构造方法定义为私有的，阻止了外部程序实例化该类，但可以在该类内部写一个静态的public方法GetInstance()，这个方法的目的就是返回一个类实例，并在此方法中，去做是否有实例化的判断。 单件模式的类图： ![](http://47.100.4.8/wp-content/uploads/2019/04/2.png)   问题：            该公司数据库拥有三张表，分别是用户表、部门表和项目表。每张表的操作都支持查询和添加功能。数据库支持mysql和sqlserver两种。结合抽象工厂模式和单件模式给出该系统的模拟代码。            在抽象工厂模式中，一个应用里一般每个产品只需要一个具体工厂的实例，因此，工厂通常最好用单件模式实现。            要求结合抽象工厂模式和单件模式，模拟公司数据库创建过程。 类图： ![](http://47.100.4.8/wp-content/uploads/2019/04/3-e1555219097900.jpg) 实现代码：

#include<iostream>

using namespace std;

//用户表
class userTable{
public:
    virtual void searchElem()=0;
    virtual void addElem()=0;
};

class mysqlUserTable:public userTable{
public:
    void searchElem(){cout<<"UserTable mysql Search"<<endl;}
    void addElem(){cout<<"UserTable mysql Add"<<endl;}
};

class sqlserverUserTable:public userTable{
public:
    void searchElem(){cout<<"UserTable sqlserver Search"<<endl;}
    void addElem(){cout<<"UserTable sqlserver Add"<<endl;}
};

//部门表
class departmentTable{
public:
    virtual void searchElem()=0;
    virtual void addElem()=0;
};

class mysqlDepartmentTable:public departmentTable{
public:
    void searchElem(){cout<<"DepartmentTable mysql Search"<<endl;}
    void addElem(){cout<<"DepartmentTable mysql Add"<<endl;}
};

class sqlserverDepartmentTable:public departmentTable{
public:
    void searchElem(){cout<<"DepartmentTable sqlserver Search"<<endl;}
    void addElem(){cout<<"DepartmentTable sqlserver Add"<<endl;}
};

//项目表
class programTable{
public:
    virtual void searchElem()=0;
    virtual void addElem()=0;
};

class mysqlProgramTable:public programTable{
public:
    void searchElem(){cout<<"ProgramTable mysql Search"<<endl;}
    void addElem(){cout<<"ProgramTable mysql Add"<<endl;}
};

class sqlserverProgramTable:public programTable{
public:
    void searchElem(){cout<<"ProgramTable sqlserver Search"<<endl;}
    void addElem(){cout<<"ProgramTable sqlserver Add"<<endl;}
};

//工厂
class IFactory{
public:
    virtual userTable* createUserTable()=0;
    virtual departmentTable* createDepartmentTable()=0;
    virtual programTable* createProgramTable()=0;
};

class mysqlFactory:public IFactory{
public:
    static mysqlFactory* GetLinstance(){
        if(_mysqlfactory == NULL){
            _mysqlfactory = new mysqlFactory();
            cout<<"mysqlFactory Create Success!"<<endl;
        }
        else{
            cout<<"mysqlFactory has existed!"<<endl;
        }
        return _mysqlfactory;
    }
    userTable* createUserTable(){return new mysqlUserTable();}
    departmentTable* createDepartmentTable() {return new mysqlDepartmentTable();}
    programTable* createProgramTable() {return new mysqlProgramTable();}
private:
    mysqlFactory(){
    }
    static mysqlFactory* _mysqlfactory;
};
mysqlFactory* mysqlFactory::_mysqlfactory = NULL;

class sqlserverFactory:public IFactory{
public:
    static sqlserverFactory* GetLinstance(){
        if(_sqlserverFactory == NULL){
            _sqlserverFactory = new sqlserverFactory();
            cout<<"sqlserverFactory Create Success!"<<endl;
        }
        else{
            cout<<"sqlserverFactory has existed!"<<endl;
        }
        return _sqlserverFactory;
    }
    userTable* createUserTable(){return new sqlserverUserTable();}
    departmentTable* createDepartmentTable() {return new sqlserverDepartmentTable();}
    programTable* createProgramTable() {return new sqlserverProgramTable();}
private:
    sqlserverFactory(){
    }
    static sqlserverFactory* _sqlserverFactory;
};
sqlserverFactory* sqlserverFactory::_sqlserverFactory = NULL;

int main(){
    //创建用户表mysql工厂
    IFactory* factory1 = mysqlFactory::GetLinstance();
    userTable* utmysql = factory1->createUserTable();
    utmysql->searchElem();
    utmysql->addElem();
    cout<<endl;
    //创建用户表sqlserver工厂
    IFactory* factory2 = sqlserverFactory::GetLinstance();
    userTable* utserver = factory2->createUserTable();
    utserver->searchElem();
    utserver->addElem();
    cout<<endl;
    //创建部门表mysql工厂
    IFactory* factory3 = mysqlFactory::GetLinstance();
    departmentTable* dtmysql = factory3->createDepartmentTable();
    dtmysql->searchElem();
    dtmysql->addElem();
    cout<<endl;
    //创建部门表sqlserver工厂
    IFactory* factory4 = sqlserverFactory::GetLinstance();
    departmentTable* dtsqlserver = factory4->createDepartmentTable();
    dtsqlserver->searchElem();
    dtsqlserver->addElem();
    cout<<endl;
    //创建项目表mysql工厂
    IFactory* factory5 = mysqlFactory::GetLinstance();
    programTable* ptmysql = factory5->createProgramTable();
    ptmysql->searchElem();
    ptmysql->addElem();
    cout<<endl;
    //创建项目表sqlserver工厂
    IFactory* factory6 = sqlserverFactory::GetLinstance();
    programTable* ptserver = factory6->createProgramTable();
    ptserver->searchElem();
    ptserver->addElem();
    return 0;
}

结果： ![](http://47.100.4.8/wp-content/uploads/2019/04/4.png)