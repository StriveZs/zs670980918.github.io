---
title: 多种群遗传算法的函数优化算法
url: 1513.html
id: 1513
categories:
  - 优化算法
  - 多种群遗传算法（MPGA）
  - 文章页
  - 算法
date: 2018-08-28 16:40:46
tags:
  - 遗传算法
  - 多种群遗传算法
  - 智能优化
  - 算法
  - MatLab
---

**多种群遗传算法的函数优化算法（MPGA）** **多种群遗传算法（MPGA）概述** MPGA在GA的基础上主要引入了一下几个概念：

*   突破GA仅靠单个群体进行遗传进化的框架，引入多个种群问题同时进行优化搜索；不同的种群赋以不用的控制参数，实现不同的搜索的目的。
*   各个种群之间通过移民算子进行联系，实现多种群的协同进化；最优解的获取是多个种群协同进化的综合结果。
*   通过人工选择算子保存各种群每个进化代中的最优个体，并作为判断算法收敛的依据。

MPGA的算法结构示意图 ![](http://47.100.4.8/wp-content/uploads/2018/08/1-1.png)   这里的SGA就是标准GA，由上图可以看出每个种群还是遵循GA中的算法准则，只不过是通过移民算子以及人工选择将最优的解结合到了一起。 各种群取不同的控制参数。交叉概率Pc和变异概率Pm的取值决定了算法全局搜索和拒不搜索能力的均衡。在GA中，交叉算子是产生新个体的主要算子，它决定了遗传算法全局搜索的能力；而变异算子只是产生新个体的辅助算子，它决定了遗传算法的局部搜索能力。大多数认为Pc在0.7~0.9最为合适，Pm在0.001~0.05之间最为合适。但是他们的取值方式还是有无数种的，对于不同的取值方式，优化结果差异也是很大的。MPGA弥补了GA的这一不足，通过多个设有不同控制参数的种群协同进化，同时兼顾了算法的全局搜索和局部搜索。 各种群是相对独立的，相互之间通过移民算子联系。移民算子将各种群在进化过程中出现的最优个体定期地（每隔一定的进化代数）引入其他的种群中，实现种群之间的信息交换。具体的操作规则是，将目标种群中的最差个体用源种群的最优个体替代。移民算子在MPGA中至关重要，如果没有银民算子，各种群之间失去联系，MPGA将等同于用不同的控制参数进行多次GA计算，从而是去了MPGA的特色。 精华种群和其他种群有很大不同。在金华的每一代，通过人工选择算子选出其他种群的 最优个体放入精华种群加以保存。精华种群不进行选择、交叉、变异等遗传操作，保证进化过程中各种群产生的最优个体不被破坏和丢失。同时，精华种群也是判断算法终止的依据。这里采用最优个体最少保持代数作为最终判断依据。这种判断充分利用了遗传算法在进化过程中的知识积累，较最大遗传代数判据更为合理。   **问题描述** 复杂二元函数求最值： **max f(x,y) = 21.5 + xsin(4πx) + ysin(20πy)** 图像生成代码：  

clear;

\[X,Y\] = meshgrid(-10:0.355:10);

Z = 21.5 + X.\*sin(4\*pi.\*X) + Y.\*sin(20\*pi.\*Y);

surf(X,Y,Z);

图像： ![](http://47.100.4.8/wp-content/uploads/2018/08/2-1.png) 由上图可以看出该函数在区间内分布着多个局部极值，这样如果使用普通的遗传算法很容易出现早熟的现象，因此多种群遗传算法比较适合。 该问题所使用到的遗传算法工具箱的函数列表：

算子

函数

功能

创建种群

Crtbp

创建基向量

适应度计算

Ranking

常用的基于秩的适应度计算

  选择函数

Select

高级选择函数

Sus

随机变异采样

Reins

一致随机和基于适应度的重插入

交叉算子

Recombin

高级重组算子

Xovsp

单点交叉

变异算子

Mut

离散变异

  **移民算子** 函数名为immigrant，函数的输入、输出参数如下：

变量名

类型

意义

输入参数

Chrom

Cell

每个元细胞单元为一个种群的编码（移民前）

ObjV

Cell

每个元细胞为一个种群所有个体的目标值（移民前）

输出参数

Chrom

Cell

每个元细胞单元为一个种群的编码（移民后）

ObjV

Cell

每个元细胞为一个种群所有个体的目标值（移民后）

代码：
```
function \[Chrom,ObjV\]=immigrant(Chrom,ObjV)
%% 移民算子
MP=length(Chrom); %得到种群个数
% 遍历每个种群寻找到其中的最优解
for i=1:MP
    \[MaxO,maxI\]=max(ObjV{i});  % 找出第i种群中最优的个体的值以及它的序号
    next_i=i+1;                % 目标种群（移民操作中） 到下一个种群
    if next_i>MP % 如果 i的值大于总的种群个数 使用取模操作回到开头
        next\_i=mod(next\_i,MP);
    end
    \[MinO,minI\]=min(ObjV{next_i});          %  找出目标种群中最劣的个体
    %% 目标种群最劣个体替换为源种群最优个体
    Chrom{next_i}(minI,:)=Chrom{i}(maxI,:);
    ObjV{next_i}(minI)=ObjV{i}(maxI); %目标值的替换
end 
```
**人工选择算子** 函数名为EliteInduvidual，函数的输入、输出参数如下：

变量名

意义

输入参数

Chrom

每个元细胞单元为一个种群的编码（移民前）

ObjV

每个元细胞为一个种群所有个体的目标值（移民前）

MaxObjV

各个种群当前最优个体的目标值（选择前）

MaxChrom

各个种群当前最优个体的编码（选择前）

输出参数

MaxObjV

各个种群当前最优个体的目标值（选择后）

MaxChrom

各个种群当前最优的编码（选择后）

代码：
```
function \[MaxObjV,MaxChrom\]=EliteInduvidual(Chrom,ObjV,MaxObjV,MaxChrom)
%% 人工选择算子
MP=length(Chrom);  %种群数
for i=1:MP
    \[MaxO,maxI\]=max(ObjV{i});   %找出第i种群中最优个体以及编号
    if MaxO>MaxObjV(i) %如果选择出来的最优个体的目标值大于当前种群最优的目标值
        MaxObjV(i)=MaxO;         %记录各种群的精华个体
        MaxChrom(i,:)=Chrom{i}(maxI,:);  %记录各种群精华个体的编码
    end
end 
```
**目标函数** 针对提出问题写出来的目标函数 代码：
```
function obj=ObjectFunction(X)
%% 待优化的目标函数
col=size(X,1); %得到个体个数
for i=1:col %计算种群每个个体对应的目标值
    obj(i,1)=21.5+X(i,1)\*sin(4\*pi\*X(i,1))+X(i,2)\*sin(20\*pi\*X(i,2));
end 

**MPGA：**

%% 2、多种群遗传算法
clear;
clc
NIND=40;               %个体数目
NVAR=2;                %变量的维数
PRECI=20;              %变量的二进制位数
GGAP=0.9;              %代沟
MP=10;                 %种群数目
FieldD=\[rep(PRECI,\[1,NVAR\]);\[-3,4.1;12.1,5.8\];rep(\[1;0;1;1\],\[1,NVAR\])\];  %译码矩阵
for i=1:MP
    Chrom{i}=crtbp(NIND, NVAR*PRECI);                       %创建初始种群
end
pc=0.7+(0.9-0.7)*rand(MP,1);    %在【0.7,0.9】范围i内随机产生交叉概率
pm=0.001+(0.05-0.001)*rand(MP,1);  %在【0.001,0.05】范围内随机产生变异概率
gen=0;  %初始遗传代数
gen0=0; %初始保持代数
MAXGEN=10;  %最优个体最少保持代数
maxY=0; %最优值
for i=1:MP
    ObjV{i}=ObjectFunction(bs2rv(Chrom{i}, FieldD));%计算各初始种群个体的目标函数值
end
MaxObjV=zeros(MP,1);           %记录精华种群
MaxChrom=zeros(MP,PRECI*NVAR); %记录精华种群的编码
% 结束条件为如果进行MAXGEN+1次优秀的迭代 则结束循环（即每次得到的最优结果都比前面的值好）
while gen0<=MAXGEN
    gen=gen+1;       %遗传代数加1
    for i=1:MP
        FitnV{i}=ranking(-ObjV{i});                      % 各种群的适应度
        SelCh{i}=select('sus', Chrom{i}, FitnV{i},GGAP); % 选择操作
        SelCh{i}=recombin('xovsp',SelCh{i}, pc(i));      % 交叉操作
        SelCh{i}=mut(SelCh{i},pm(i));                    % 变异操作
        ObjVSel=ObjectFunction(bs2rv(SelCh{i}, FieldD)); % 计算子代目标函数值
        \[Chrom{i},ObjV{i}\]=reins(Chrom{i},SelCh{i},1,1,ObjV{i},ObjVSel);    %重插入操作
    end
    \[Chrom,ObjV\]=immigrant(Chrom,ObjV);     % 移民操作
    \[MaxObjV,MaxChrom\]=EliteInduvidual(Chrom,ObjV,MaxObjV,MaxChrom);     % 人工选择精华种群
    YY(gen)=max(MaxObjV);    %找出精华种群中最优的个体
    if YY(gen)>maxY   %判断当前优化值是否与前一次优化值相同
        maxY=YY(gen); %更新最优值
        gen0=0;
    else
        gen0=gen0+1; %最优值保持次数加1
    end
end
%% 进化过程图
plot(1:gen,YY);
xlabel('进化代数')
ylabel('最优解变化')
title('MPGA进化过程')


%% 输出最优解
\[Y,I\]=max(MaxObjV);    %找出精华种群中最优的个体
X=(bs2rv(MaxChrom(I,:), FieldD));   %最优个体的解码解
disp(\['最优值为：',num2str(Y)\])
disp(\['对应的自变量取值：',num2str(X)\]) 
```
结果： 最优值为：38.8503 对应的自变量取值：11.6255      5.72504 ![](http://47.100.4.8/wp-content/uploads/2018/08/3-1.png)