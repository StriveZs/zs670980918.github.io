---
title: 用遗传算法（GA）求一元函数最小值
url: 1437.html
id: 1437
categories:
  - GA
  - MatLab
  - 优化算法
  - 文章页
  - 算法
date: 2018-07-10 13:09:42
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180710130810.png) **遗传算法简介：** 该算法是一种进化算法，其基本原理是效仿生物界中的“物竞天择，适者生存”的演化原则，遗传算法是把问题参数编码为染色体，然后利用迭代的方式进行选择、交叉以及变异等运算来交换群中染色体的信息最终生成符合优化目标的染色体。   在遗传算法中，染色体对应的是数据或数组，通常是由一维的串结构数据来表示，串各个位置对应的基因的取值。基因组成的串就是染色体、或者称为基因型个体。一定数量的个体组成了群体。群体中个体的数目称为群体大小，也成为群体规模，而各个个体对应的适应程度叫做适应度。 **  遗传算法的步骤：**

*   编码：将解空间的解数据表示成遗传算法的基因型串数据，串数据的组合便构成了解
*   初始种群产生：随机产生N个基因型串数据，这N个染色体构成一个群体
*   适应度评估：评价染色体个体的优劣性
*   选择：从群体中选择出好的染色体，让它们生存下去，这样有机会把优良的基因遗传给子代。
*   交叉：使用基因型的交叉可以得到新一代的个体
*   变异：：变异首先在群体种随机选择一个个体，对于选中的个体以一定的概率随机地改变串结构数据中的某个值。

**在Matlab中可以使用遗传算法工具箱（gatbx），关于工具箱安装我会出一个具体的博文。** 介绍一下遗传算法工具箱的主要函数列表：

函数分类

函数

功能  

  选择函数

reins

一致随机和基于适应度的重插入

rws

轮盘选择

select

高级选择例程

sus

随机便利采样

            交叉算子

recdis

离散重组

recint

中间重组

recline

线性重组

recmut

具有变异特征的线性重组

recombin

高级重组算子

xovdp

两点交叉算子

xovdprs

减少代理的两点交叉

xovmp

通常多点交叉

xovsh

洗牌交叉

xovshrs

减少代理的洗牌交叉

xovsp

单点交叉

xovsprs

减少代理的单点交叉

  变异算子

mut

离散变异

mutate

高级变异函数

mutbga

减少代理的单点交叉

子种群的支持

migrate

在子种群间交换个体

实用函数

bs2rv

二进制串到实值的转换

rep

矩阵的复制

  创建种群

crtbase

创建基向量

crtbp

创建任意离散随机种群

crtrp

创建实值初始种群

硬度计算

ranking

基于排序的适用度分配

scaling

比率适应度计算

  先用遗传算法解决简单的一元函数求最小值的问题：![](http://47.100.4.8/wp-content/uploads/2018/07/1-4.png) 参数设置

种群大小

最大遗传代数

个体长度

代沟

交叉概率

变异概率

40

20

20

0.95

0.7

0.01

代沟：上一代总数为100，通过选择之后剩下80（舍弃20），代沟 = 80/100 = 0.8 **这里给出代码和注解：**

clc
clear all
close all
%画出函数图
figure(1);  %设置控制窗口的名
hold on ; %保存axes内图像用的，确保之前的图像不会被新图像覆盖
lb = 1;
ub = 2;  %设置变量范围\[1,2\]
ezplot('sin(10\*pi\*x)/x',\[lb,ub\]);  %根据变量范围画图
xlabel('自变量/x')  %设置xy轴名称
ylabel('函数值/y')

%定义遗传算法参数
Nind = 40;  %种群大小
Lind = 20; %个体基因长度
MaxGen = 30; %遗传代数（迭代次数）
GGAP = 0.95 %代沟
px = 0.7; %交叉概率
pm = 0.01; %bianyigailv
FieldD = \[Lind;lb;ub;1;0;1;1\] %设置矩阵转换器配置
trace = zeros(2,MaxGen);  %用于记录每一代的最优解以及对应的x的值

%初始化
Chrom = crtbp(Nind,Lind)  %创建任意离散随机种群
gen = 0; %迭代计数器
x = bs2rv(Chrom,FieldD); %将初始化中群转换为十进制
ObjV = sin(10\*pi\*x)./x;  %计算初始种群的对应的函数值
%进行迭代优化
while gen<MaxGen
    FitnV = ranking(ObjV);  %计算适应度
    SelCh = select('sus',Chrom,FitnV,GGAP);  %根据代沟选择遗传下来的个体数=（种群总书*代沟）
    SelCh = recombin('xovsp',SelCh,px);  %进行交叉重组
    SelCh = mut(SelCh,pm);  %进行变异，只是有一定几率变异
    x = bs2rv(SelCh,FieldD); %重新计算新生成的子代的十进制群
    ObjVSel = sin(10\*pi\*x)./x;  %计算子代的函数值
    \[Chrom,ObjV\] = reins(Chrom,SelCh,1,1,ObjV,ObjVSel); %重新将子代插入到父代中，得到新的种群
    x = bs2rv(Chrom,FieldD); %求出新的种群对应的函数值
    gen = gen+1; %迭代次数+1
    %获得没代最优解以及序号 
    \[Y,I\] = min(ObjV);  %Y为最优解  I为个体的序号
    trace(1,gen) = x(I); %记录最优解对应x的值
    trace(2,gen) = Y;  %记录下最优解的值
end

plot(trace(1,:),trace(2,:),'bo');   %根据每代的最优点画出图形
grid on;
plot(x,ObjV,'b*');  %画出最后一代的种群
hold off;

%画出进化图
figure(2);
plot(1:MaxGen,trace(2,:));
grid on;
xlabel('遗传代数');
ylabel('解的变化');
title('进化过程');
bestY = trace(2,end);
bestX = trace(1,end);
fprintf(\['最优解：\\nx=',num2str(bestX),'\\ny=',num2str(bestY),'\\n'\]);

**结果：（这里是进行30次的结果）** ![](http://47.100.4.8/wp-content/uploads/2018/07/2-2.png) ![](http://47.100.4.8/wp-content/uploads/2018/07/3-1.png) 有上面的结果可以看出随着迭代次数的增加，结果趋于稳定，我自己也试了迭代100次的结果到后面几乎就是一条平的线。