---
title: 2-3-4树学习（续）
url: 1234.html
id: 1234
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-22 23:41:15
tags:
  - C/C++
  - 2-3-4树
---

向四结点的插入节点的情况： 第二种情况： 向3 key结点插入，父结点也是3 key结点的处理情况。 如图： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-7.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/2-7.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/3-6.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/4-6.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/5-4.png) 主要核心的思想是：向3 key结点插入数值，父结点也为3 key结点的话，则父结点也要进行中间值提到父结点的父结点的操作，知道结点不再是3 key值结点为止。   下面给出2-3-4数创建的过程（大家可自行分析理解我个人认为已经很好理解了） 如图： ![](http://47.100.4.8/wp-content/uploads/2018/05/6-3.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/7-3.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/8-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/9-1.png) 最后会形成一个所有高度都一样的树： ![](http://47.100.4.8/wp-content/uploads/2018/05/10-1.png) 在很多数据的情况下： 2-3-4树的效率比平衡二叉树要好的很多。 2-3-4的高度的最坏情况（全是2-node），也就相当于演变成了平衡二叉树 ： 相当于平衡二叉树 lgN 2-3-4树高度的最好情况（全是4-node），log4 N = 1/2 lg N   删除操作：要保证结点在同一高度，有必要时要进行合并 如图： ![](http://47.100.4.8/wp-content/uploads/2018/05/11-2.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/12-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/13-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/14-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/15.png) 在这里要感谢：[https://www.jianshu.com/p/37c845a5add6](https://www.jianshu.com/p/37c845a5add6) [http://www.cnblogs.com/nullzx/p/6111175.html](http://www.cnblogs.com/nullzx/p/6111175.html) 两位博主 提供的讲解，上面的图均取自二者的博文，再次感谢。   C++实现难点：要有三种结点分别有三个两个一个键值，要进行他们之间的转换，以及处理所以比较麻烦。 由于代码比较难于实现所里这里只进行了分析。 为了以后的红黑树做准备。   因此这给出伪代码： 结点数据结构：
```
//1键值的结点

struct Node1{

    Elem data1;

    Node1 *rNode; //右子节点

    Node1 *lNode; //左子节点

};

Node1 root; //根结点一定是为1个键值的结点

//2键值的结点

struct Node2{

    Elem data1;

    Elem data2;

    Node2 *rNode;

    Node2 *zNode;//中间子节点

    Node2 *lNode;

};

//3键值的结点

struct Node3{

    Elem data1;

    Elem data2;

    Elem data3;

    Node3 *rNode;

    Node3 *rzNode; //右二子节点

    Node3 *lzNode;  //左二子节点

    Node3 *lNode;

};

    插入操作的伪代码：  

void insert(Key key,Elem Val)

{

    Node x=root;

    while (x.getTheCorrectChild(key) != null) //查找到子节点为止 如果不为空则一直继续向下寻找

    {

        x = x.getTheCorrectChild(key);  //跳转到下一个节点根据给出的key

        if (x.is4Node()) //如x所在键值是3个的结点还要在插入一个则将该节点分解，

            x.split();

    }

    if (x.is2Node())  //如果为两键值节点

        x.make3Node(key, val); //则进行插入操作

    else if (x.is3Node())   //如果为三键值结点

        x.make4Node(key, val); //则进行插入操作

}
```