---
title: STL之heap
url: 1185.html
id: 1185
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-13 21:30:44
tags:
  - C/C++
  - STL
  - heap
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180507183124.png) STL中并没有把heap作为一种容器组件，heap的实现亦需要更低一层的容器组件（诸如list,array,vector）作为其底层机制。Heap是一个类属算法，包含在algorithm头文件中。虽然STL中关于heap默认调整成的是大顶堆，但却可以让用户利用自定义的compare\_fuction函数实现大顶堆或小顶堆。heap的低层机制vector本身就是一个类模板，heap基于vector便实现了对各种数据类型（无论基本数据类型还是用户自定义的数据类型）的堆排（前提是用户自定义的数据类型要提供比较机制compare\_fuction函数）。   包含在头文件**#include<****algorithm****>**  下面的\_First与\_Last为可以随机访问的迭代器（指针），\_Comp为比较函数（仿函数），其规则——如果函数的第一个参数小于第二个参数应返回true，否则返回false。   建立堆 make\_heap（\_First,\_Last,\_Comp） 默认是建立最大堆。对int类型，可以在第三个参数传入great<int>（）得到最小堆。   在堆中添加数据 push\_heap（\_First,\_Last） 要先在容器中加入数据，再调用push\_heap（）   在堆中删除数据 pop\_heap（\_First,\_Last） 要先调用pop\_heap（）再在容器中删除数据   堆排序 sort\_heap（\_First,\_Last） 排序之后就不再是一个合法的heap了   总结： **这里在通过对写下面代码的过程中，对heap有了更进一步的了解。** **个人认为这个堆相关的操作就是算法的集合。** **需要注意的是要创建一个动态容器（vector）：vector<int>*test1=new vector<int>(MAXN);** **以及创建迭代器：vector<int>::iterator pos;方便在遍历容器元素时使用。** **将容器构建成一个堆 make_heap（）将容器放进去。注意由于这里是指针创建的动态容器，所以在调用容器成员时 使用->进行访问。** **在插入数据时，要先在容器中进行数据插入，然后在堆中插入使用push_heap（）** **在删除数据时，要先从堆中删除数据使用pop_heap（），然后在容器中删除数据** **由于容器中没有排序成员函数，所以这里就体现出了堆中堆排序的重要性。** **sort_heap****（）** 代码：
```
#include<iostream>
#include<vector>
#include<algorithm>
#include<functional>

using namespace std;


int main()
{
    int MAXN = 20;
    int a\[MAXN\];
    int i;
    //创建一个随机数组
    for(int i=0;i<MAXN;i++)
        a\[i\] = rand()%(MAXN*2);
    cout<<"创建一个堆"<<endl;
    //创建动态vector容器 并对vector建堆
    vector<int>*test1=new vector<int>(MAXN);
    vector<int>::iterator pos;
    test1->assign(a,a+MAXN);
    make_heap(test1->begin(),test1->end());  //用test1建堆
    for(pos = test1->begin();pos!=test1->end();pos++)
        cout<<*pos<<" ";
    cout<<endl;
    cout<<"在堆中进行插入数据:"<<endl;
    //对堆进行新数据插入  要现在容器中加入，在调用push_heap（）
    test1->push_back(25);
    push_heap(test1->begin(),test1->end());
    for(pos = test1->begin();pos!=test1->end();pos++)
        cout<<*pos<<" ";
    cout<<endl;
    //删除数据  先调用pop_heap（）从堆中删除，然后再在容器中删除
    cout<<"删除堆中的数据："<<endl;
    pop_heap(test1->begin(),test1->end());  //从堆中弹出一个元素
    test1->pop_back();  //然后在容器中删除该元素
    push_heap(test1->begin(),test1->end());
    test1->pop_back();
    for(pos = test1->begin();pos!=test1->end();pos++)
        cout<<*pos<<" ";
    cout<<endl;
    //堆排序
    cout<<"进行堆排序之后的结果："<<endl;
    sort_heap(test1->begin(),test1->end());
    for(pos = test1->begin();pos!=test1->end();pos++)
        cout<<*pos<<" ";
    cout<<endl;
    return 0;
}
```
截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/453445324324.png)