---
title: 使用遗传算法工具箱解决二元函数求极值问题
url: 1450.html
id: 1450
categories:
  - GA
  - MatLab
  - 优化算法
  - 文章页
  - 算法
date: 2018-07-13 11:43:37
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180706191552.png) **计算二元函数的最大值** **二元函数为：![](http://47.100.4.8/wp-content/uploads/2018/07/11.png)** **基础参数配置为：**

种群大小

最大遗传代数

个体长度

代沟

交叉概率

变异概率

40

100

40（两个自变量每个长20）

0.95

0.7

0.01

代码：

clc
clear all
close all
%%画出函数图
figure(1);  %设置为窗口1
lbx = -2;  %自变量x的范围
ubx = 2;
lby = -2; %自变量y的范围
uby = 2;
%%画有两个变量的函数并且要根据范围去画，因此使用ezmesh
ezmesh('y\*sin(2\*pi\*x)+x\*cos(2\*pi\*y)',\[lbx,ubx,lby,uby\],50);
hold on;
%%定义遗传算法参数
Nind = 40;  %种群大小为40
Lind = 20; %两个变量合在一起的基因长度为40  x为20  y为20
MaxGen = 100; %遗传最大代数
GGAP = 0.95; %代沟
px = 0.7; %交叉概率
pm = 0.01; %变异概率
trace = zeros(3,MaxGen); %用来存储每一代中的最优结果
FieldD = \[Lind Lind;lbx lby;ubx uby;1 1;0 0;1 1;1 1\];  %设置好FieldD参数,因为是两个变量所有x y要分开设置
%%初始化
Chrom = crtbp(Nind,Lind*2);  %随机生成初始种群
gen = 0; %种群迭代计数器
XY = bs2rv(Chrom,FieldD);  %生成的XY为一个Nind行 两列的数组 前一列是x的值，后一列是y的值
x = XY(:,1);  %分别存储x和y的值
y = XY(:,2);
ObjV = y.\*sin(2\*pi\*x)+x.\*cos(2\*pi\*y);  %进行计算函数值  采用.*是进行矩阵计算
while gen<MaxGen
    FitnV = ranking(-ObjV);  %进行适应度计算
    SelCh = select('sus',Chrom,FitnV,GGAP); %通过轮盘赌算法并且根据适应度和代沟来选择留下的染色体
    SelCh = recombin('xovsp',SelCh,px);  %选出来的染色体进行交叉;
    SelCh = mut(SelCh,pm); %再进行变异
    XY = bs2rv(SelCh,FieldD); %将子代转换为十进制
    x = XY(:,1);
    y = XY(:,2);
    ObjVSel = y.\*sin(2\*pi\*x)+x.\*cos(2\*pi\*y); %计算子代的函数值
    \[Chrom,ObjV\] = reins(Chrom,SelCh,1,1,ObjV,ObjVSel); %基于适应度的选择，将子代重新插入到父代中
    XY = bs2rv(Chrom,FieldD); %重新计算，方便在写入trace时使用
    gen = gen + 1; %迭代次数+1
    \[Y,I\] = max(ObjV);
    trace(1:2,gen) = XY(I,:);  %记录下来每次迭代最优的xy
    trace(3,gen) = Y; %记录下来最优值
end
plot3(trace(1,:),trace(2,:),trace(3,:),'bo'); %在figure1画出每代的最优点
grid on;
plot3(XY(:,1),XY(:,2),ObjV,'bo');  %画出最后一代的种群
hold off
%%画出进化图
figure(2);
plot(1:MaxGen,trace(3,:));
grid on;
xlabel('遗传代数');
ylabel('解的变化');
title('进化过程');
bestZ = trace(3,end);
bestX = trace(1,end);
bestY = trace(2,end);
fprintf(\['最优解：\\nX=',num2str(bestX),'\\nY=',num2str(bestY),'\\n最大值为=',num2str(bestZ)\]);

结果： ![](http://47.100.4.8/wp-content/uploads/2018/07/12.png) ![](http://47.100.4.8/wp-content/uploads/2018/07/13.png)