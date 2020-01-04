---
title: 地址变换算法
url: 1305.html
id: 1305
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-06-05 17:47:31
tags:
  - C/C++
  - 地址变换算法
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180605173814.png) 地址变换算法：根据当前的地址使用公式，绝对地址计算公式：块号*块的长度+页内偏移量 来得到物理地址从而实现从逻辑地址向物理地址的转换。 页表的形式： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180605174311.png) 思想： 如果匹配的情况下： 在内存中存在则直接计算绝对地址使用公式：块号*块的长度+页内偏移量 如果不匹配且在页表中存在： 将产生缺页中断，并且修改对应的页表项。 如果不匹配且在页表中不存在： 输出在页表项没有的提示。   算法代码：
```
//地址变换算法
void Transform()
{
    for(int i=0;i<m;i++)
    {
        cout<<"第"<<i+1<<"次！"<<endl;
        int t=-1;
        for(int j=0;j<num;j++)
        {
            if(yebiao\[j\].YeHao == xulie\[i\])
            {
                t = j;
                break;
            }
        }
        if(yebiao\[t\].BiaoZhi==1&&yebiao\[t\].Flag==0)
        {
            cout<<"    页面已经存入内存但是修改位并未修改，进行修改！~"<<endl;
            yebiao\[t\].Flag = 1;
            cout<<"绝对地址："<<yebiao\[t\].YeHao * 300 + yebiao\[t\].DiZhi<<endl;
            cout<<endl;
            continue;
        }
        if(yebiao\[t\].BiaoZhi==1&&yebiao\[t\].Flag==1)
        {
            cout<<"    页面已经进入内存"<<endl;
            cout<<"绝对地址："<<yebiao\[t\].YeHao * 300 + yebiao\[t\].DiZhi<<endl;
            cout<<endl;
            continue;
        }
        if(xulie\[i\]>=num)
        {
            cout<<"    序列值大于页表项中最大的页面号"<<endl;
            cout<<endl;
            continue;
        }
        cout<<"    页面不在内存！,产生缺页中断"<<endl;
        cout<<"    将页面装入内存！"<<endl;
        yebiao\[t\].BiaoZhi = 1;
        yebiao\[t\].Flag = 1;
        cout<<endl;
    }
}
```
使用到的数据结构：
```
struct YeBiao{
    int YeHao; //页号
    int BiaoZhi; //标志
    int ZhuCunHao; //页对应的主存号
    int Flag; //表示该页调入主存后是否修改过的标志
    int DiZhi;  //外存地址
}yebiao\[num\];
```