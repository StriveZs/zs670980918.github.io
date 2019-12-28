---
title: 基于GA的TSP算法
url: 1497.html
id: 1497
categories:
  - GA
  - TSP问题
  - 优化算法
  - 文章页
  - 算法
date: 2018-08-19 17:43:12
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/08/QQ图片20180819172202.png) **TSP问题简介：** 旅行商问题，即TSP问题（Traveling Salesman Problem）是数学领域中著名问题之一。假设有一个旅行商人要拜访N个城市，他必须选择所要走的路径，路径的限制是每个城市只能拜访一次，而且最后要回到原来出发的城市。路径的选择目标是要求得的路径路程为所有路径之中的最小值。TSP问题是一个[NPC](https://baike.baidu.com/item/NPC/658479)问题，即为在最坏的情况下的时间复杂度随着问题规模的增大按指数方式增长。 这里使用遗传算法（GA）来解决这个问题 **问题描述：**已知N个城市之间相互的距离，某一旅行商从某个城市出发访问每个城市一次且仅访问一次，最后回到出发城市，如何安排才使其所走路线最短，实质上就是寻找一条最短的路径能够遍历N个城市。 **问题介绍：** 这里通过给定十四个城市的坐标来寻找一条最短路径 ![](http://47.100.4.8/wp-content/uploads/2018/08/QQ图片20180819172609.png) 算法流程： ![](http://47.100.4.8/wp-content/uploads/2018/08/12.png) 使用遗传算法实现：

*   **编码**

采用整数排列的方式，对于本案例中十四个城市的TSP问题，将染色体分别十四段，每一段对应一个城市的编号，例如对十个城市的TSP问题{1,2,3,4,5,6,7,8,9,10}，则|1|2|3|5|7|4|10|8|9|6|8|是一个合法的染色体。

*   **种群初始化**

在完成染色体编码以后，必须产生一个初始种群作为起始种群解，所以首先需要决定初始化种群的数目一般根据经验得到，一般情况下种群的数量视城市规模的大小而确定，其取值在50~200之间浮动

*   **适应度函数**

设|k1|k2|……|kn|为一个采用整数编码的染色体，Dkikj为城市ki到城市kj的距离，则该个体的适应度为 即为恰好走完n个城市，再回到出发城市的距离的倒数。优化目标是选择适应度值尽可能大的染色体，这样也就是走的距离短的染色体，这样的染色体更好。

*   **选择操作**即从旧群体中以一定概率选择个体到新群体中，个体被选中的概率跟适应度值有关，个体适应度越大，被选中的概率越高
*   **交叉操作**

采用部分映射杂交，确定交叉操作的父代，将父代样本两两分组，每组重复一下过程，进行交叉，如r1=4，r2=7 ![](http://47.100.4.8/wp-content/uploads/2018/08/13.png) 交叉后被交换的位置基因不改变，其他段的基因由于和被交换的段的基因冲突，要采用部分映射的方法消除冲突（利用中间段）消除冲突后的结果为： ![](http://47.100.4.8/wp-content/uploads/2018/08/14.png)、

*   **变异操作**

变异策略是采取随机选取两个点，将其对换位置。随机产生在\[1,10\]之间的两个整数r1和r2，确定两个基因后对换两个基因的的位置。 如： ![](http://47.100.4.8/wp-content/uploads/2018/08/15.png)

*   **进化逆转操作**

为改善遗传算法的局部搜索能力，在选择、变异、交叉之后引进连续多次的进化逆转操作。这里的进化是指逆转算子的单方向性，只有经过逆转后，适应度值有提高的才能接受下来，否则逆转无效。 随机战胜两个\[1,10\]之间的数，将其对应的基因对换位置 如r1=4，r2=7 ![](http://47.100.4.8/wp-content/uploads/2018/08/16.png) 下面给出MatLab代码： **首先给出主函数GA_TSP**

%遗传算法求解TSP问题
%输入：
%D       距离矩阵
%NIND    为种群个数
%X       参数是中国34个城市的坐标(初始给定)
%MAXGEN  为停止代数，遗传到第MAXGEN代时程序停止,MAXGEN的具体取值视问题的规模和耗费的时间而定
%m       为适值淘汰加速指数,最好取为1,2,3,4,不宜太大
%Pc      交叉概率
%Pm      变异概率
%输出：
%R       为最短路径
%Rlength 为路径长度
clear
clc
close all
%% 加载数据
% 加载所有城市的坐标从1-14
X = \[\[16.4700000000000,96.1000000000000;16.4700000000000,94.4400000000000;20.0900000000000,92.5400000000000;22.3900000000000,93.3700000000000;25.2300000000000,97.2400000000000;22,96.0500000000000;20.4700000000000,97.0200000000000;17.2000000000000,96.2900000000000;16.3000000000000,97.3800000000000;14.0500000000000,98.1200000000000;16.5300000000000,97.3800000000000;21.5200000000000,95.5900000000000;19.4100000000000,97.1300000000000;20.0900000000000,92.5500000000000\]\];
D=Distanse(X);  %生成距离矩阵  具体的是根据坐标X 将以上信息转换为一个对称的距离矩阵
N=size(D,1);    %城市个数
%% 遗传参数
NIND=100;       %种群大小  代表有Nind种路径
MAXGEN=200;     %最大遗传代数
Pc=0.9;         %交叉概率
Pm=0.05;        %变异概率
GGAP=0.9;       %代沟
%% 初始化种群
Chrom=InitPop(NIND,N); %根据种群大小和基因长度
%% 画出随机解的路径图
DrawPath(Chrom(1,:),X) %将随机初始化种群的第一种解用来画出路径图
pause(0.0001)  %用来放慢速度  和 C++ 中的Time类似
%% 输出随机解的路径和总距离
disp('初始种群中的一个随机值:')
OutputPath(Chrom(1,:));  %输出路径
Rlength=PathLength(D,Chrom(1,:)); %根据距离矩阵和路线来计算路径长度
disp(\['总距离：',num2str(Rlength)\]);
disp('~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~')
%% 优化
gen=0;  %初始化迭代代数
figure;
hold on;box on
xlim(\[0,MAXGEN\])
title('优化过程')
xlabel('代数')
ylabel('最优值')
ObjV=PathLength(D,Chrom);  %计算每一代的路径长度
preObjV=min(ObjV); %得到最小的路径长度
while gen<MAXGEN
    %% 计算适应度
    ObjV=PathLength(D,Chrom);  %计算每一代的路径长度
    % fprintf('%d   %1.10f\\n',gen,min(ObjV))
    line(\[gen-1,gen\],\[preObjV,min(ObjV)\]); % 用来在图上画出适应度减少的过程
    pause(0.0001) % 延迟效果
    preObjV=min(ObjV); % 得到最小的路径长度
    FitnV=Fitness(ObjV);  % 计算适应度（路径越长倒数越小，方便选择）
    %% 选择
    SelCh=Select(Chrom,FitnV,GGAP); %根据适应度和代沟进行子代的选择
    %% 交叉操作
    SelCh=Recombin(SelCh,Pc);
    %% 变异
    SelCh=Mutate(SelCh,Pm);
    %% 逆转操作
    SelCh=Reverse(SelCh,D);
    %% 重插入子代的新种群
    Chrom=Reins(Chrom,SelCh,ObjV);
    %% 更新迭代次数
    gen=gen+1 ;
end
%% 画出最优解的路径图
ObjV=PathLength(D,Chrom);  %计算路径长度
\[minObjV,minInd\]=min(ObjV);
DrawPath(Chrom(minInd(1),:),X)
%% 输出最优解的路径和总距离
disp('最优解:')
p=OutputPath(Chrom(minInd(1),:));
disp(\['总距离：',num2str(ObjV(minInd(1)))\]);
disp('-------------------------------------------------------------')

**计算距离的函数：**

%% 计算两两城市之间的距离
%输入 a  各城市的位置坐标
%输出 D  两两城市之间的距离
function D=Distanse(a)
row=size(a,1); %得到城市的个数
D=zeros(row,row); %初始化一个全为0的距离矩阵
for i=1:row  %每个城市所对应的距离矩阵的那一行
    for j=i+1:row %遍历该行出该城市之外往后的所有城市
        D(i,j)=((a(i,1)-a(j,1))^2+(a(i,2)-a(j,2))^2)^0.5;  %根据坐标计算距离
        D(j,i)=D(i,j); % 实现对称
    end
end

**初始化种群的函数：**

%% 初始化种群
%输入：
% NIND：种群大小
% N：   个体染色体长度（这里为城市的个数）  
%输出：
%初始种群
function Chrom=InitPop(NIND,N)
Chrom=zeros(NIND,N);%初始一个全0位的矩阵用于存储种群
for i=1:NIND %遍历每个染色体（个体）
    Chrom(i,:)=randperm(N);%随机生成初始种群  randperm的作用是生成N个由1-N构成的序列（里面元素不能重复）
end

**画出城市之间路径的函数：**

%% 画路径函数
%输入
% Chrom  待画路径   
% X      各城市坐标位置
function DrawPath(Chrom,X)
R=\[Chrom(1,:) Chrom(1,1)\]; %一个随机解(个体) 并且将基因中首个城市添加到基因末尾 用来构成一个循环
% 开始画图
figure;
hold on
plot(X(:,1),X(:,2),'o','color',\[0.5,0.5,0.5\])
plot(X(Chrom(1,1),1),X(Chrom(1,1),2),'rv','MarkerSize',20)
% 将每个城市对应的点画出来
for i=1:size(X,1)
    text(X(i,1)+0.05,X(i,2)+0.05,num2str(i),'color',\[1,0,0\]);
end
A=X(R,:);
row=size(A,1);
% 根据得到的R序列进行连线
for i=2:row
    \[arrowx,arrowy\] = dsxy2figxy(gca,A(i-1:i,1),A(i-1:i,2));%坐标转换
    annotation('textarrow',arrowx,arrowy,'HeadWidth',8,'color',\[0,0,1\]);
end
hold off
xlabel('横坐标')
ylabel('纵坐标')
title('轨迹图')
box on

**计算该种路径的总距离的函数：**

%% 计算各个体的路径长度
% 输入：
% D     两两城市之间的距离
% Chrom 个体的轨迹
function len=PathLength(D,Chrom) 
\[row,col\]=size(D); %得到距离矩阵的长宽
NIND=size(Chrom,1); %得到种群的总个数
len=zeros(NIND,1); %初始化一个用来存储距离的矩阵
for i=1:NIND
    p=\[Chrom(i,:) Chrom(i,1)\]; %得到该基因对应的城市路线
    i1=p(1:end-1);
    i2=p(2:end);
    len(i,1)=sum(D((i1-1)*col+i2)); %进行距离计算
end

**输出路径的函数：**

%% 输出路径函数
%输入：R 路径
function p=OutputPath(R)
R=\[R,R(1)\]; %同样要构成一个城市循环 从A->X->……->A 
N=length(R);  %得到城市总数
p=num2str(R(1));  % 强制类型转换
for i=2:N
    p=\[p,'—>',num2str(R(i))\];
end
disp(p)

**适应度计算函数：**

%% 适配值函数     
%输入：
%个体的长度（TSP的距离）
%输出：
%个体的适应度值
function FitnV=Fitness(len)
FitnV=1./len; %倒数计算

**选择函数：**

%% 选择操作
%输入
%Chrom 种群
%FitnV 适应度值
%GGAP：代沟
%输出
%SelCh  被选择的个体
function SelCh=Select(Chrom,FitnV,GGAP)
NIND=size(Chrom,1); %得到种群的染色体个数
NSel=max(floor(NIND*GGAP+.5),2); %通过代沟计算能够保留下的来的个体
ChrIx=Sus(FitnV,NSel); %进行选择
SelCh=Chrom(ChrIx,:);

Sus函数：

% 输入:
%FitnV  个体的适应度值
%Nsel   被选择个体的数目
% 输出:
%NewChrIx  被选择个体的索引号
function NewChrIx = Sus(FitnV,Nsel)
\[Nind,ans\] = size(FitnV); %得到种群个体个数
cumfit = cumsum(FitnV); %依次累加适应度并输出 每次累加的内容 从小到大
trials = cumfit(Nind) / Nsel * (rand + (0:Nsel-1)'); %计算出可以选择出适当个数的染色体的适应度标值
Mf = cumfit(:, ones(1, Nsel));
Mt = trials(:, ones(1, Nind))';
\[NewChrIx, ans\] = find(Mt < Mf & \[ zeros(1, Nsel); Mf(1:Nind-1, :) \] <= Mt); %根据适应度标志选择能够遗传下来的个体
\[ans, shuf\] = sort(rand(Nsel, 1));
NewChrIx = NewChrIx(shuf);

**交叉操作函数：**

%% 交叉操作
% 输入
%SelCh  被选择的个体
%Pc     交叉概率
%输出：
% SelCh 交叉后的个体
function SelCh=Recombin(SelCh,Pc)
NSel=size(SelCh,1); %得到被选择之后种群的个数
for i=1:2:NSel-mod(NSel,2)
    if Pc>=rand %交叉概率Pc
        \[SelCh(i,:),SelCh(i+1,:)\]=intercross(SelCh(i,:),SelCh(i+1,:)); %如果满足交叉概率
    end
end

%输入：
%a和b为两个待交叉的个体
%输出：
%a和b为交叉后得到的两个个体

function \[a,b\]=intercross(a,b)
L = length(a); %得到个体的长度
r1 = randsrc(1,1,\[1:L\]); %表示产生1行1列在区间{1，L}之间的随机数
r2 = randsrc(1,1,\[1:L\]); %产生第二个位置
if r1 ~= r2  %~= 为不等于的意思
    a0=a;b0=b;
    s=min(\[r1,r2\]);
    e=max(\[r1,r2\]);
    for i=s:e
        a1=a;b1=b;
        %将对应的位置进行交换
        a(i)=b0(i);
        b(i)=a0(i);
        x=find(a==a(i));
        y=find(b==b(i));
        i1=x(x~=i);
        i2=y(y~=i);
        %处理如果该染色体中存在该基因
        if ~isempty(i1)
            a(i1)=a1(i);
        end
        if ~isempty(i2)
            b(i2)=b1(i);
        end
    end
end

**变异操作函数：**

%% 变异操作
%输入：
%SelCh  被选择的个体
%Pm     变异概率
%输出：
% SelCh 变异后的个体
function SelCh=Mutate(SelCh,Pm)
\[NSel,L\]=size(SelCh); %得到遗传之后的种群个体个数和基因长度
for i=1:NSel
    if Pm>=rand %如果随机数满足变异概率则进行变异
        R=randperm(L); %随机一个新的序列
        SelCh(i,R(1:2))=SelCh(i,R(2:-1:1)); %将该序列插入到已有的种群中
    end
end

**逆转操作函数：**

%% 进化逆转函数
%输入
%SelCh 被选择的个体
%D     个城市的距离矩阵
%输出
%SelCh  进化逆转后的个体
function SelCh=Reverse(SelCh,D)
%该函数的具体操作是随机选两个基因的位置进行交换，这样有利于基因的多样性
\[row,col\]=size(SelCh);
ObjV=PathLength(D,SelCh);  %计算路径长度
SelCh1=SelCh;
for i=1:row
    r1=randsrc(1,1,\[1:col\]);%随机位置1
    r2=randsrc(1,1,\[1:col\]);%随机位置2
    mininverse=min(\[r1 r2\]);%找到谁大谁小
    maxinverse=max(\[r1 r2\]);
    SelCh1(i,mininverse:maxinverse)=SelCh1(i,maxinverse:-1:mininverse); %进行交换
end
ObjV1=PathLength(D,SelCh1);  %计算路径长度
index=ObjV1<ObjV;
SelCh(index,:)=SelCh1(index,:);

**重新插入新代数的函数：**

 %% 重插入子代的新种群
 %输入：
 %Chrom  父代的种群
 %SelCh  子代种群
 %ObjV   父代适应度
 %输出
 % Chrom  组合父代与子代后得到的新种群
function Chrom=Reins(Chrom,SelCh,ObjV)
NIND=size(Chrom,1); % 得到旧的种群个体个数
NSel=size(SelCh,1); % 得到新的种群个体个数
\[TobjV,index\]=sort(ObjV); %按照路径长度进行排序
Chrom=\[Chrom(index(1:NIND-NSel),:);SelCh\]; %进行插入操作

结果： 初始种群中的一个随机值: 13—>12—>9—>6—>8—>11—>5—>10—>1—>3—>14—>2—>7—>4—>13 总距离：65.9898 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 最优解: 12—>6—>5—>4—>3—>14—>2—>1—>10—>9—>11—>8—>13—>7—>12 总距离：29.3405 **随机生成的路径图：** ![](http://47.100.4.8/wp-content/uploads/2018/08/1.png) **最优结果的路径图：** ![](http://47.100.4.8/wp-content/uploads/2018/08/3.png) **迭代优化过程：** ![](http://47.100.4.8/wp-content/uploads/2018/08/2.png) End！