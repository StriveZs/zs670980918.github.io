---
title: 基于遗传算法和非线性规划的函数寻优算法
url: 1455.html
id: 1455
categories:
  - MatLab
  - 优化算法
  - 基于遗传算法和非线性规划的函数寻优算法
  - 文章页
  - 算法
date: 2018-07-15 11:37:08
tags:
---

**非线性规划研究一个n元实函数在一组等式或不等式的约束条件下的极值问题。**

非线性规划函数： 函数fmincon是MatLab最优化工具箱中求解非线性规划问题的函数，它从一个预估值触发，搜索约束条件下非线性多元函数的最小值。 函数fmincon的**约束条件**为： ![](http://47.100.4.8/wp-content/uploads/2018/07/111.png) 其中，**x、b、beq、lb和ub是矢量，A和Aeq为矩阵；c（x）和ceq（x）返回矢量的函数；f（x）、c（x）和ceq（x）是非线性函数。** **函数fmincon（fun，x0，A，b，Aeq，beq，lb，ub）** 其中lb和ub分别为x的下界和上界。当函数输入参数不包括A、b、Aeq、beq时，默认A=0、b=0，Aeq=\[ \]，beq=\[ \]   遗传算法从随机产生的初始解开始搜索，通过一定的选择、交叉、变异操作逐步迭代以产生新的解。群体种的每个个体代表问题的一个解，成为染色体，染色体的好坏用适应度值来衡量，根据适应度的好快从上一代中选择一定数量的优秀个体，通过交叉、变异来形成下一代群体。经过若干代迭代之后，收敛于最好的染色体。（但不一定是问题的最优解）   非线性规划算法大多采用梯度下降的方法求解，局部搜索能力强，但是全局搜索能力差，遗传算法则是全局搜索能力强，局部搜索能力差，因此二者集合能够得到问题的最优解。   **采用遗传算法和非线性规划的方式求解的例子：** 其中x1、x2、x3、x4、x5是0~0.9*π之间的实数。 该函数的最小值为-2，最小值的位置为（π/2，π/2，π/2，π/2，π/2）   非线性规划遗传算法的流程图： ![](http://47.100.4.8/wp-content/uploads/2018/07/112.png) N为一个固定值，当进化代数为N的倍数时采用非线性寻优的方法加快进化，非线性寻优利用当前染色体值采用函数fmincon寻找问题的局部最优值。   算法思路：

1.  种群初始化

采用的编码方式有：位串编码、Grey编码、实数编码（浮点数编码）、多级参数编码、有序串编码、结构式编码等。

2.  适应度函数

因为这个例子中求得是函数最小值所有，把函数值的倒数最为个体的适应度值。目标函数值越小的个体，适应度越大，个体越优。

3.  选择操作

从旧群体中选择出优良个体组成新的种群，以繁殖到下一代，常用的选择算法有：轮盘赌算法、锦标赛算法等，常用的是轮盘赌算法。即基于适应度比例的选择策略 个体被选中的概率为：![](http://47.100.4.8/wp-content/uploads/2018/07/113.png)，Fi为个体的适应度值

4.  交叉操作

从种群中随机选择两个个体，通过两个染色体的交换组合，把父串的优秀特征遗传给子串，从而产生新的优秀个体。由于采用实数编码，因此采用实数交叉法：第k个单色提的ak和第L个染色体的al在j位的交叉操作

5.  变异操作

目的是维护种群的多样性，从种群中随机选择一个个体，选择个体中的一点进行变异以产生更优秀的个体。

6.  非线性寻优

每进化一定代数后，以所得到的结果为初始值，采用fmincon进行局部寻优，并把局部寻优的结果作为染色体继续进化 **实现：** 计算目标值的函数文件  

function y = fun(x)

y=-5\*sin(x(1))\*sin(x(2))\*sin(x(3))\*sin(x(4))\*sin(x(5))-sin(5\*x(1))\*sin(5\*x(2))\*sin(5\*x(3))\*sin(5\*x(4))\*sin(5\*x(5))+8;



选择函数

%%选择操作  该函数对每一代种群中的染色体进行选择，以进行后面的交叉和变异

function ret = select(indivduals,sizepop) %indivduals为种群信息   sizepop为种群规模

%indivduals input :种群信息

%sizepop input :种群规模

%opts input :选择方法的选择

%ret output :经过选择后的种群

indivduals.fitness = 1./(indivduals.fitness); %计算适应度

sumfitness = sum(individuals.fitness); %计算适应度之和

sumf = indivduals.fitness./sumfitness;  %计算适应度占比

index = \[\];   %创建一个空数组 用来存储选择出来的染色体的下标

for i=1:sizepop  %循环sizepop

    pick = rand;  %将pick赋值为一个随机小数范围在0-1

    while pick == 0  %设置一下防止rand 出来的值使pick为0

        pick = rand;

    end

    for j = 1 :sizepop %遍历每一个染色体的适应度占比

        pick = pick - sumf(j); %如果pick - 某个染色体的适应度占比小于0 则将该染色体对应的下表添加到index中

        if pick < 0

            index = \[index j\];

            break;

        end

    end

end

indivduals.chrom = indivduals.chrom(index,:);  %将选择出来的染色体存到一个子种群中

indivduals.fitness = indivduals.fitness(index);  %将对应的适应度也存储到一起

ret = indivduals;

交叉操作函数：  

%%交叉操作

function ret = Cross(pl,lenchrom,chrom,sizepop,bound)

%pl input :交叉概率

%lenchrom input :染色体的长度

%chrom input:染色体种群

%sizepop input:种群规模

%ret ouput:交叉后的染色体

for i=1:sizepop     %是否进行交叉由交叉概率决定

    %随机选择两个染色体进行交叉

    pick = rand(1,2);  %产生两个0-1的随机数

    while prod(pick) == 0

        pick = rand(1,2);

    end

    index = ceil(pick.*sizepop);  %将随机到的数转换为对应的染色体编号  ceil（x）是取比x大的最小整数

    %交叉概率决定是否进行交叉

    pick  = rand;  %随机出来一个交叉概率

    while pick == 0

        pick = rand;

    end

    %如何随机出来的交叉概率大于给定的交叉概率则结束本次循环

    if pick > pcross

        continue;

    end

    flag = 0;

    while flag == 0

        %随机选择交叉位置

        pick = rand;

        while pick ==0

            pick = rand ;

        end

        pos = ceil(pick.*sum(lenchrom));  %将随机出来的数转换为染色体对应的某个基因

        pick = rand;  %随即一个数用于在交叉时选择基因位置时作为参数

        v1 = chrom(index(1),pos);

        v2 = chrom(index(2),pos);

        %交叉公式

        chrom(index(1),pos) = pick * v2 + (1-pick) * v1;

        chrom(index(2),pos) = pick * v1 + (1-pick) * v2;

        flag1 = test(lenchrom,bound,chrom(index(1),:),fcode);

        flag2 = test(lenchrom,bound,chrom(index(2),:),fcode);

        if flag1*flag2 == 0

            flag = 0;

        else

            flag =1;

        end

    end

end

ret = chrom;

变异操作：

%%变异操作

function ret = Mutation(pm,lenchrom,chrom,sizepop,bound)

%本函数完成变异操作

%pcorss input :变异概率

%lenchrom input : 染色体长度

%chrom input:染色体群'

%sizepop input :种群规模

%pop input:当前种群的进化代数和最大的进化代数信息

% ret output:变异后的染色体

for i =1;sizepop

    %随机选择一个染色体进行变异

    pick = rand;

    while pick == 0

        pick = rand;

    end

    index = ceil(pick * sizepop);  %将随机出来的数转换为对应的染色体的编号

    %决定该轮是否进行变异

    pick = rand;

    if pick > pm

        continue;

    end

    flag = 0;

    while flag == 0

        %随机一个变异位置

        pick = rand;

        while pick == 0

            pick = rand;

        end

        pos = ceil(pick * sum(lenchrom));  %转换为对应染色体基因的位置

        v = chrom(i,pos);  %得到该位置的值

        v1 = v - bound(pos,1);

        v2 = bound(pos,2) - v;

        pick = rand;  %变异开始

        if pick > 0.5  %变异分为两种情况

            delta = v2 * (1 - pick((1 - pop(1)/pop(2))^2));

            chrom (i,pos) = v + delta;

        else

            delta = v1 * (1 - pick((1 - pop(1)/pop(2))^2));

            chrom (i,pos) = v - delta;

        end

        flag = test(lenchrom,bound,chrom(i,:),fcode);

    end

end

ret = chrom;

随机编码函数：

function ret=Code(lenchrom,bound)

%本函数将变量编码成染色体，用于随机初始化一个种群

% lenchrom   input : 染色体长度

% bound      input : 变量的取值范围

% ret        output: 染色体的编码值



flag=0;

while flag==0

    pick=rand(1,length(lenchrom));

    ret=bound(:,1)'+(bound(:,2)-bound(:,1))'.*pick; %线性插值

    flag=test(lenchrom,bound,ret);             %检验染色体的可行性

end

非线性优化函数：

function ret = nonlinear(chrom,sizepop)



for i=1:sizepop

    x=fmincon(inline('-5\*sin(x(1))\*sin(x(2))\*sin(x(3))\*sin(x(4))\*sin(x(5))-sin(5\*x(1))\*sin(5\*x(2))\*sin(5\*x(3))\*sin(5\*x(4))\*sin(5\*x(5))'),chrom(i,:)',\[\],\[\],\[\],\[\],\[0 0 0 0 0\],\[2.8274 2.8274 2.8274 2.8274 2.8274\]);

    ret(i,:)=x';

end

主函数：

%% 清空环境

clc

clear

warning off



%% 遗传算法参数

maxgen=30;                         %进化代数

sizepop=100;                       %种群规模

pcross=\[0.6\];                      %交叉概率

pmutation=\[0.01\];                  %变异概率

lenchrom=\[1 1 1 1 1\];              %变量字串长度

bound=\[0 0.9\*pi;0 0.9\*pi;0 0.9\*pi;0 0.9\*pi;0 0.9*pi\];  %变量范围



%% 个体初始化

individuals=struct('fitness',zeros(1,sizepop), 'chrom',\[\]);  %种群结构体

avgfitness=\[\];                                               %种群平均适应度

bestfitness=\[\];                                              %种群最佳适应度

bestchrom=\[\];                                                %适应度最好染色体

% 初始化种群

for i=1:sizepop

    individuals.chrom(i,:)=Code(lenchrom,bound);       %随机产生个体

    x=individuals.chrom(i,:);  %得到每一个个体的值

    individuals.fitness(i)=fun(x);                     %进行个体适应度的计算

end



%对初代进行操作   找最好的染色体

\[bestfitness bestindex\]=min(individuals.fitness);   %得到本代中计算出目标函数值的最小的值

bestchrom=individuals.chrom(bestindex,:);  %得到最好的染色体

avgfitness=sum(individuals.fitness)/sizepop; %计算总染色体的平均适应度

% 记录每一代进化中最好的适应度和平均适应度

trace=\[\];



%% 进化开始

for i=1:maxgen

   

    % 选择操作

    individuals=Select(individuals,sizepop);  %选择出好的个体组成一个种群

    avgfitness=sum(individuals.fitness)/sizepop; %计算出子代种群的平均适应度

    % 交叉操作

    individuals.chrom=Cross(pcross,lenchrom,individuals.chrom,sizepop,bound);

    % 变异操作

    individuals.chrom=Mutation(pmutation,lenchrom,individuals.chrom,sizepop,\[i maxgen\],bound);

   

    if mod(i,10)==0  %如果进化代数为10的倍数则进行非线性优化

        individuals.chrom=nonlinear(individuals.chrom,sizepop);

    end

   

    % 计算进行交叉变异之后的新种群适应度

    for j=1:sizepop

        x=individuals.chrom(j,:);

        individuals.fitness(j)=fun(x);

    end

   

    %找到最小和最大适应度的染色体及它们在种群中的位置

    \[newbestfitness,newbestindex\]=min(individuals.fitness);

    \[worestfitness,worestindex\]=max(individuals.fitness);

    % 代替上一次进化中最好的染色体

    if bestfitness>newbestfitness  %如果上一代中最好的适应度大于当前代中最好的适应度则将它代替

        bestfitness=newbestfitness;

        bestchrom=individuals.chrom(newbestindex,:);

    end

    individuals.chrom(worestindex,:)=bestchrom;

    individuals.fitness(worestindex)=bestfitness;

   

    avgfitness=sum(individuals.fitness)/sizepop;

   

    trace=\[trace;avgfitness bestfitness\]; %记录每一代进化中最好的适应度和平均适应度

end

%进化结束



%% 结果显示

figure

\[r c\]=size(trace);

plot(\[1:r\]',trace(:,1),'r-',\[1:r\]',trace(:,2),'b--');

title(\['函数值曲线  ' '终止代数＝' num2str(maxgen)\],'fontsize',12);

xlabel('进化代数','fontsize',12);ylabel('函数值','fontsize',12);

legend('各代平均值','各代最佳值','fontsize',12);

ylim(\[1.5 8\])

disp('函数值                   变量');

% 窗口显示

disp(\[bestfitness x\]);

grid on

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/07/114.png) ![](http://47.100.4.8/wp-content/uploads/2018/07/115.png) 根据数值分析也可以看出随着迭代次数的增加，最好适应度的值变化减小，直道不在变化