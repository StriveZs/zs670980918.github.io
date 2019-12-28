---
title: C++之array
url: 1197.html
id: 1197
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-16 23:56:20
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) array是序列容器的一种，它类似一般数组，是在连续的内存上来存储数据，并且array的长度是固定的不可改变的。 这里需要的注意的是：array中元素可以被修改，但是不能在array上进行数据插入和删除。 那么问题来了为什么要使用array呢？ array相比较于一般数组，它提供了更好、更安全的接口，它除了具有一般数组的灵活性，还具有和一般数组相近的性能优势。   相比较于vector来说新创建的vector数组不会包含元素，而新创建的array就会包含固定数目的元素，并且这些元素都会被初始化。 因此在创建array数组时就要声明数组的大小，且后面不能再改变。   构造语句为： array<类型，元素个数>数组名称（={初值}）； 如果没有初值则默认为0，注意：能够用一个array数组来初始化另一个array数组，但是需要保证两个array数组的大小相同。 同样可以使用swap（）语句来对两个array数组进行交换。   array的成员函数fill（）可以用来将array中的所有元素赋值为一个相同的值。 array<int,3>arr1; arr1.fill(2);  这样就将arr1中所有的数据都改为了1.   array的成员函数有size（）可以获得当前数组的元素个数，方便对数组的遍历。   array的成员还有begin（）和end（）分别获得头尾成员。   简答使用：

#include<iostream>
#include<array>


using namespace std;

int main()
{
    array<int,5> test1={1,2,3,4,5};
    array<int,5> test2=test1;
    array<int,5> test3(test1);
    cout<<"输出array数组test:"<<endl;
    for(int i=0;i<test1.size();i++)
        cout<<test1\[i\]<<" ";
    cout<<endl;
    cout<<test1.begin()<<" "<<test1.end()<<endl;
    return 0;
}

  具体的使用结果请自行尝试，因为我的凉了。。 大体上是对的。我编译会出错，度娘上面讲的也不是很清楚，所以这次是在抱歉了。 感觉这次有点少，其实我是想和valarray一起发的，但是还没弄完。所以就先发这个了。下次发valarray