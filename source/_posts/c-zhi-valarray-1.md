---
title: C++之valarray
url: 1206.html
id: 1206
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-18 23:05:26
tags:
  - C/C++
  - valarray
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) valarray使用： valarray类似vector，也是一个模板类，其主要被用来对一系列元素进行高速的数字计算。 但是它和vector还是有区别的： 1、valarray定义了一组在两个相同长度和相同类型的valarray类对象之间的数字计算，例如xarr = cos(yarr) + sin(yarr)； 2、通过重载operater\[\]，可以返回valarray的相关信息（valarray其中某个元素的引用、特定下标的值或者其某个子集）。 它支持很多数值数组操作，如求数组总和，最大值，最小值等。 通过引用#include<valarray>来使用 对于上面的对数组进行整体操作的方式和python中numpy数组的使用挺相似的。   构造函数： valarray<类型>（test1）名称； //初始长度为0 valarray<类型>名称（n）； //初始长度为n valarray<类型>test2（test1）； //调用复制构造函数   成员函数： test1.apply（函数）；  //将指定的函数应用于valarray的每个元素。即对test1中每个元素都调用用函数 test1.cshift（）；  //将valarray中的所有元素按指定的位置顺序移动。 例如： test1.cshift（4）； 为将test1中所有元素都右移四位 test1.max（）;  //找到该数组中最大元素 test1.min（）； //找到该数组中最小元素 test1.resize（）；  //将valarray中的元素数量更改为指定的数字，根据需要添加或删除元素。 test1.shift（）； //将valarray中的所有元素移位指定的位置数。 test1.size（）； //得到当前valarray数组中元素个数 test1.sum（）； //确定非零长度的valarray中所有元素的总和。 但是遗憾的是它没有push_back（） begin（） end（）insert（）等成员函数。 对于数组的赋值在下面的例子中会使用。   同样valarray也对各种运算符进行了重载 运算符 !  //获得valarray中每个元素的逻辑NOT值的一元运算符。 %=  //通过指定的valarrayor或元素类型的值来获得数组元素的剩余部分。 &=  //获取数组中元素的按位与，或者与指定的数组中的相应元素或元素类型的值进行比较。 >>=  //将valarray操作数的每个元素的位右移位指定数量的位置，或者通过第二个valarray指定的元素方式右移位。   <<=  //将valarray操作数的每个元素的位向左移位指定数量的位置，或者由第二个valarray指定的元素方式量左移位。   *=  //将指定的valarray的元素或元素类型的值（元素值）乘以一个操作数。 + //将指定的valarray元素或元素类型的值（元素）和操作数进行相加。

*   //将减号应用于valarray中的每个元素的一元运算符。即为负号

-= //将指定的valarray元素或元素类型的值（元素）和操作数进行相减。 /= //用指定valarray的元素或元素类型的值元素分隔操作数valarray。 =  //将元素分配给valarray，其值可以直接指定，也可以作为其他某些数据项的一部分或由slice\_array，gslice\_array，mask\_array或indirect\_array指定。 \[ \]  //返回对指定索引或指定子集的元素或其值的引用。 ^=  //获取具有指定valarray或元素类型值的数组的元素明确的逻辑或运算符（XOR） |=   //获取数组中元素的按位或或者与指定的数组中的相应元素或元素类型的值。 ~   //一个一元运算符，用于获取valarray中每个元素的按位非值。   slice类用法： 该类主要配合 valarray 类使用，可以从 valarray 中提取子数组 slice( ); slice( size __ _t __StartIndex _,// 截取数组的开始位置 const valarray<size __ _t> __Len _, 2，// 子数组的最大长度 const valarray<size __ _t> __Stride// __相隔多少个元素选中一个_ ); **Gslice** **类用法** Gslice 类的用法和slice 基本相同，只是它截取的是循环子串，当母串进行一次提取后的字串元素数目达不到要求时，gslice 会将提取后的母串继续组合进行提取直到满足要求或者母串被提取完了 公共函数( 对数组的操作) abs 对数组的每一个元素取绝对值 acos 返回每个元素的反余弦值 asin  返回每个元素的反正弦值 atan  返回每个元素的正切值 atan2 笛卡尔正切值 cos 余弦值 cosh  双曲线余弦值 exp 返回自然指数E^x log 返回自然对数 log10 返回以10 为底的返回自然对数 exp 返回x^y sin 正弦值 sinh 双曲线正弦值 .sqrt 开方 tan 正切值 tanh 反正切值   使用：
```
#include<iostream>

#include<valarray>



using namespace std;



int main()

{

    valarray<int>a;  //定义一个长为0的valarray数组

    valarray<int>b(1,5);  //用1初始化b  b的元素个数为5

    valarray<int>c(b);  //用b来初始化c

    int data\[5\]={1,2,3,4,5};

    //valarray<int>d(data,3); //也成立

    valarray<int>d(data,5);  //去data数组中前三个元素来初始化d数组

    cout<<"b中元素的总和："<<b.sum()<<endl;

    cout<<"输出d中最大元素："<<d.max()<<endl;

    cout<<"d中元素："<<endl;

    for(int i=0;i<d.size();i++)

        cout<<d\[i\]<<" ";

    cout<<endl;

    cout<<"没进行+=之前b中元素："<<endl;

    for(int i=0;i<b.size();i++)

        cout<<b\[i\]<<" ";

    cout<<endl;

    b+=d;

    cout<<"之后b中元素："<<endl;

    for(int i=0;i<b.size();i++)

        cout<<b\[i\]<<" ";

    cout<<endl;

    valarray<int>e(0,5);

    cout<<"使用=运算符之后："<<endl;

    b=e;

    cout<<"b中元素："<<endl;

    for(int i=0;i<b.size();i++)

        cout<<b\[i\]<<" ";

    cout<<endl;

    valarray<int>f(data,4);

    cout<<"f中元素："<<endl;

    for(int i=0;i<f.size();i++)

        cout<<f\[i\]<<" ";

    cout<<endl;

    //使用slice切割

    slice t(2,4,1);

    a=f\[t\];

    return 0;

}
```
    这里有一个问题就是slice的使用类似切片操作，但是我明明编译没有错误，但是就是显示不出来结果，暂时没办法解决，感觉是我c++编译器版本的问题。