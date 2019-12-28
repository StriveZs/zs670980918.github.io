---
title: 使用SGA对多元函数进行优化
url: 1518.html
id: 1518
categories:
  - GA
  - 优化算法
  - 文章页
  - 算法
date: 2018-08-29 21:11:40
tags:
---

**这是是通过使用SGA来解决之前在多种群遗传算法的函数优化中提出的问题，以便来做对比，以此来看出多种群遗传算法相较于普通的遗传算法的优势。** 这里在描述一下之前的问题： 求解该max f(x,y) = 21.5 + xsin(4πx) + ysin(20πy)函数的最大值 函数图像如下所示： ![](http://47.100.4.8/wp-content/uploads/2018/08/2-1.png) 图像生成代码在之前已经给出了，这里就不给了。 接下来是使用标准的遗传算法来解决上面的问题 代码：

clear;
%clc
pc=0.7;     % 交叉概率
pm=0.05; % 变异概率
%定义遗传算法参数
NIND=40;        %个体数目
MAXGEN=500;     %最大遗传代数
NVAR=2;               %变量的维数
PRECI=20;             %变量的二进制位数
GGAP=0.9;             %代沟
trace=zeros(MAXGEN,1); %记录优化轨迹
FieldD=\[rep(PRECI,\[1,NVAR\]);\[-3,4.1;12.1,5.8\];rep(\[1;0;1;1\],\[1,NVAR\])\]; %建立区域描述器
Chrom=crtbp(NIND, NVAR*PRECI);                       %创建初始种群
gen=0;                                               %代计数器   
ObjV=ObjectFunction(bs2rv(Chrom, FieldD));%计算初始种群个体的目标函数值
\[maxY,I\]=max(ObjV); %最优值
X=bs2rv(Chrom, FieldD);
maxX=X(I,:);
while gen<MAXGEN                                     %迭代
    FitnV=ranking(-ObjV);                            %分配适应度值(Assign fitness values)
    SelCh=select('sus', Chrom, FitnV, GGAP);         %选择
    SelCh=recombin('xovsp', SelCh, pc);              %重组
    SelCh=mut(SelCh,pm);                             %变异
    ObjVSel=ObjectFunction(bs2rv(SelCh, FieldD));           %计算子代目标函数值
    \[Chrom ObjV\]=reins(Chrom, SelCh, 1, 1, ObjV, ObjVSel);  %重插入
    gen=gen+1;           %代计数器增加
    % 最优值更新
    if maxY<max(ObjV)
        \[maxY,I\]=max(ObjV);
        X=bs2rv(Chrom, FieldD);
        maxX=X(I,:);
    end
    trace(gen,1)=maxY;
end

%% 进化过程图
plot(1:gen,trace(:,1));
hold on
xlabel('进化代数');
ylabel('最优解变化');
title('SGA进化过程');

%% 输出最优解
disp(\['最优值为：',num2str(maxY)\]);
disp(\['对应的自变量取值：',num2str(maxX)\]); 

结果： ![](http://47.100.4.8/wp-content/uploads/2018/08/67.png) 根据迭代次数就可以明显的看出多种群遗传算法比标准的遗传算法更加的少，多种群遗传算法能够更快的完成迭代得到最优值。 而且多种群遗传算法比标准遗传算法得到的结果更加精确。