---
title: 模拟退火算法（SA）解决TSP问题
url: 1529.html
id: 1529
categories:
  - SA
  - TSP问题
  - 优化算法
  - 文章页
  - 算法
date: 2018-09-17 17:57:36
tags:
  - SA
  - TSP
  - 优化算法
  - 算法那
---

![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180917174510.png)

**使用SA来解决TSP问题**

模拟退火算法基本原理： 模拟退火（SA）算法的出发点是基于物理中固体物质的退火过程与一般的组合优化问题之间的相似性。模拟退火法是一种通用的优化算法，其物理退火过程由以下三部分组成：

*   加温过程。其目的是增强粒子的热运动，使其偏离平衡位置。当温度足够高时，固体将熔为液体，从而消除系统原先存在的非均匀状态。
*   等温过程。对于与周围环境交换热量而温度不变的封闭系统，系统状态的自发变化总是朝自由能减少的方向进行的，当自由能达到最小时，系统达到平衡状态。
*   冷却过程。使粒子热运动减弱，系统能量下降，得到晶体结构。

其中，加温过程对应算法的设定初温，等温过程对应算法的Metropolis抽样过程，冷却过程对应控制参数的下降。这里能量的变化就是目标函数，要得到的最优解就是能量低态。Metropolis准则是SA算法收敛于全局最优解的关键所在，Metropolis准则以一定的概率接受恶化解，这样就使算法跳离局部最优的陷阱。 模拟退火算法为求解传统方法难处理的TSP问题提供了一个有效的途径和通用框架，并逐渐发展成一种迭代自适应启发式概率性搜索算法。模拟退火算法可以用求解不同的非线性问题，对不可微甚至不连续的函数优化，能以较大概率求得全局优化解，该算法还具有较强的鲁棒性、全局收敛性、隐含并行性及广泛的适应性，并且能处理不同类型的优化设计变量（离散的、连续的和混合型的），不需要任何的辅助信息，对目标函数和约束函数没有任何要求。利用Metropolis算法并适当地控制温度下降过程，在优化问题中具有很强的竞争力。   SA算法实现过程如下（以最小化问题为例） ：

*   初始化：取初始温度T0足够大，令T=T0，任取初始解S1，确定每个T时的迭代次数，即Metropolis链长L
*   对当前温度T和k=1,2，……，L重复步骤（3）~（5）
*   对当前解S1随机扰动产生一个新解S2
*   计算S2的增量df=f（S2）-f（S1），其中f（S1）为S1的代价函数
*   若df<0，则接受S2作为新的当前解， 即S1=S2；否则计算S2的接受概率exp（-df/T），即随机产生（0,1）区间上均匀分布的随机数rand，若exp（-df/T）>rand，也接受S2作为新的当前解，S1=S2；否则保留当前解S1。
*   如果满足终止条件Stop，则输出当前解S1为最优解，结束程序。终止条件Stop通常为：在连续若干个Metropolis链中新解S2都没有被接受时终止算法，或是设定结束温度。否则按衰减函数衰减T后返回步骤（2）。

以上步骤称为Metropolis过程。逐渐降低控制温度，重复Metropolis过程，直至满足结束准备则Stop，求出最优解。   算法流程： ![](http://47.100.4.8/wp-content/uploads/2018/09/321.png) 模拟退火算法实现： （1）控制参数的设置 需要设置的主要参数有降温速率q、初始温度T0、结束温度Tend以及链长L。 （2）初始解 对于n个城市的TSP问题，得到的解就是对1~n的一个排序，其中每个数字为对应城市的编号，如对10个城市的TSP问题{1,2,3,4,5,6,7,8,9,10}，则|1|3|5|2|4|9|7|8|6|10|就是一个合法的解，采用产生随机排列的方法产生一个初始的解S。 （3）解变换生成新解 通过对当前解S1进行变换，产生新的路径数组即新解，这里采用的变换是产生随机数的方法来产生将要交换的两个城市，用二邻域变换法产生新的路径，即新的可行解S2。 （4）Metropolis准则fdf 若路径长度函数为f（S），则当前解的路径为f（S1），新解的路径为f（S2），路径差为 df=f（S2）-f（S1），则Metropolis准则为： ![](http://47.100.4.8/wp-content/uploads/2018/09/333.png) 如果df<0，则以概率1接收新的路径了；否则以概率exp（-df/T）接收新的路径。 （5）降温 利用降温速率q进行降温，即T=qT，若T小于结束温度，则停止迭代输出当前状态，否则继续迭代。   程序实现 主程序代码：
```
clc;
clear;
close all;
%%
tic
T0=1000;   % 初始温度
Tend=1e-3;  % 终止温度
L=500;    % 各温度下的迭代次数（链长L）
q=0.9;    %降温速率

%% 加载数据
load CityPosition1;
%%
D=Distanse(X);  %计算距离矩阵
N=size(D,1);    %城市的个数
%% 初始解
S1=randperm(N);  %随机产生一个初始路线

%% 画出随机解的路径图
DrawPath(S1,X)
pause(0.0001)
%% 输出随机解的路径和总距离
disp('初始种群中的一个随机值:')
OutputPath(S1);  %输出用->表示的路径
Rlength=PathLength(D,S1); %输出路径总长度
disp(\['总距离：',num2str(Rlength)\]);

%% 计算迭代的次数Time
%参考下面代码来修改solve式子
%syms x
%eqn = sin(x) == 1;
%solx = solve(eqn,x)
syms x;
eqns = 1000*(0.9)^x == Tend; %Time表示通过计算得到的迭代次数
Time=ceil(double(solve(eqns,x)));  %ceil（小数）为朝着大整数 取整
count=0;        %迭代计数
Obj=zeros(Time,1);         %目标值矩阵初始化
track=zeros(Time,N);       %每代的最优路线矩阵初始化
%% 迭代
while T0>Tend
    count=count+1;     %更新迭代次数
    temp=zeros(L,N+1);
    for k=1:L
        %% 产生新解
        S2=NewAnswer(S1);
        %% Metropolis法则判断是否接受新解
        \[S1,R\]=Metropolis(S1,S2,D,T0);  %Metropolis 抽样算法
        temp(k,:)=\[S1 R\];          %记录下一路线的及其路程
    end
    %% 记录每次迭代过程的最优路线
    \[d0,index\]=min(temp(:,end)); %找出当前温度下最优路线
    if count==1 || d0<Obj(count-1)
        Obj(count)=d0;           %如果当前温度下最优路程小于上一路程则记录当前路程
    else
        Obj(count)=Obj(count-1);%如果当前温度下最优路程大于上一路程则记录上一路程
    end
    track(count,:)=temp(index,1:end-1);  %记录当前温度的最优路线
    T0=q*T0;     %降温
    fprintf(1,'%d\\n',count)  %输出当前迭代次数
end
%% 优化过程迭代图
figure
plot(1:count,Obj)
xlabel('迭代次数')
ylabel('距离')
title('优化过程')

%% 最优解的路径图
DrawPath(track(end,:),X)

%% 输出最优解的路线和总距离
disp('最优解:')
S=track(end,:);
p=OutputPath(S);
disp(\['总距离：',num2str(PathLength(D,S))\]);
disp('-------------------------------------------------------------')
toc

Distance函数：

function D=Distanse(a)
%% 计算两两城市之间的距离
%输入 a  各城市的位置坐标
%输出 D  两两城市之间的距离
row=size(a,1);  %得到城市总数
D=zeros(row,row);  %初始化城市距离矩阵
%计算每一个城市和其他城市之间的距离
for i=1:row
    for j=i+1:row
        D(i,j)=((a(i,1)-a(j,1))^2+(a(i,2)-a(j,2))^2)^0.5;
        D(j,i)=D(i,j);
    end
end

DrawPath函数：

function DrawPath(Chrom,X)
%% 画路径函数
%输入
% Chrom  待画路径   
% X      各城市坐标位置
R=\[Chrom(1,:) Chrom(1,1)\]; %一个随机解(个体)  构成路径的循环
figure;
hold on
%% 画点操作
plot(X(:,1),X(:,2),'o','color',\[0.5,0.5,0.5\])
plot(X(Chrom(1,1),1),X(Chrom(1,1),2),'rv','MarkerSize',20) %标出起始点的位置
for i=1:size(X,1)
    text(X(i,1)+0.05,X(i,2)+0.05,num2str(i),'color',\[1,0,0\]);
end
%% 画线操作
A=X(R,:);
row=size(A,1); %得到路径上经过城市数（包括头尾城市）
for i=2:row
    \[arrowx,arrowy\] = dsxy2figxy(gca,A(i-1:i,1),A(i-1:i,2));%坐标转换
    annotation('textarrow',arrowx,arrowy,'HeadWidth',8,'color',\[0,0,1\]);
end
%% 构图信息
hold off
xlabel('横坐标')
ylabel('纵坐标')
title('轨迹图')
box on 

Output函数：

function p=OutputPath(R)
%% 输出路径函数
%输入：R 路径
R=\[R,R(1)\];
N=length(R);
p=num2str(R(1));
for i=2:N
    p=\[p,'—>',num2str(R(i))\];
end
disp(p) 

PathLength函数：

function len=PathLength(D,Chrom)
%% 计算各个体的路径长度
% 输入：
% D     两两城市之间的距离
% Chrom 个体的轨迹
\[row,col\]=size(D); %得到距离矩阵的长和宽
NIND=size(Chrom,1); %城市总数 也就得到了总的路径条数
len=zeros(NIND,1);
for i=1:NIND %遍历每条路径
    p=\[Chrom(i,:) Chrom(i,1)\]; %构成经过城市循环
    i1=p(1:end-1);
    i2=p(2:end);
    len(i,1)=sum(D((i1-1)*col+i2)); %路径累加
end 

Metropolis函数：

function \[S,R\]=Metropolis(S1,S2,D,T)
%% 输入
% S1：  当前解
% S2:   新解
% D:    距离矩阵（两两城市的之间的距离）
% T:    当前温度
%% 输出
% S：   下一个当前解
% R：   下一个当前解的路线距离
%%
%首先根据距离矩阵分别计算两个解的路径长度
R1=PathLength(D,S1);  %计算路线长度
N=length(S1);         %得到城市的个数

R2=PathLength(D,S2);  %计算路线长度
dC=R2-R1;   %计算能力之差
if dC<0       %如果能力降低 接受新路线
    S=S2;
    R=R2;
elseif exp(-dC/T)>=rand   %以exp(-dC/T)概率接受新路线
    S=S2;
    R=R2;
else        %不接受新路线
    S=S1;
    R=R1;
End 
```
  随机的路径图： ![](http://47.100.4.8/wp-content/uploads/2018/09/333333.png) 优化后的路径图： ![](http://47.100.4.8/wp-content/uploads/2018/09/555555555555.png) 优化过程； ![](http://47.100.4.8/wp-content/uploads/2018/09/666666666666.png) 初始种群中的一个随机值: 7—>5—>14—>2—>3—>12—>10—>6—>8—>11—>13—>9—>4—>1—>7 总距离：69.3773 最优解: 9—>11—>8—>13—>7—>12—>6—>5—>4—>3—>14—>2—>1—>10—>9 总距离：29.3405 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- 时间已过 3.718870 秒。   附加：CityPosition包 16.4700000000000        96.1000000000000 16.4700000000000        94.4400000000000 20.0900000000000        92.5400000000000 22.3900000000000        93.3700000000000 25.2300000000000        97.2400000000000 22                                         96.0500000000000 20.4700000000000        97.0200000000000 17.2000000000000        96.2900000000000 16.3000000000000        97.3800000000000 14.0500000000000        98.1200000000000 16.5300000000000        97.3800000000000 21.5200000000000        95.5900000000000 19.4100000000000        97.1300000000000 20.0900000000000        92.5500000000000