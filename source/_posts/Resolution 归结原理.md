---
title: Resolution 归结原理

categories:
  - 高级人工智能
  - 知识点

tags:
  - Resolution

mathjax: true
---

# Resolution 归结原理
## 和取范式
满足一种特殊形式的sentences，conjunction of disjunctions of literals(文字)，一个原子命题的符号A或者他前面加上一个 `$\neg A $`都称为**文字**。  
disjunction of literals形式如:均用析取符号`$\vee$`连接，比如`$ A\vee B \vee C $`  
conjunction of disjunction of literals(和取范式): 多个disjunction of literals用合取符号连接`$\wedge`，比如:`$(A\vee B\vee C)\wedge (D\vee \neg E)$`  
上面和的和取范式称为CNF。  

语义等价`$\equiv$` 表示两个sentences可以互相转换(语义等价)，比如`$A \equiv B$`, 可以参考knowledge 1中提供的语义等价公式表来进行转换。  

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/wquYOk.png)

任何范式都是可以转换其他语义等价的合取范式。  
将knowledge base中的任意一个sentence转换为一个CNF(通过语义等价)，然后将合取去掉，分成一个个disjunction of literals，将分拆开的DOL(disjunction of literals简写)组成一个新的knowledge base。这样将一个原来的一个knowledge base转换为了一个新的 knowledge base(KB简写)。  
即`$KB \equiv KB' $`  

## 归结

`$A, \neg A $`称为互补文字.

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/hUS3vR.png)

若`$ l_{i} $`和`$ m_{j} $`为互补文字，则可以把`$ l_{1}\vee l_{i}, m_{j}\vee m_{1} $`使用归结原理可以将`$ l_{i} $`和`$ m_{j} $`去掉可以化简为`$l_{1}\vee m_{1} $`从上述的式子中去掉.(**归结规则**)  
每一次归结只能拿一对来进行归结，然后下一次还可以拿另外一对进行归结.  

对于一个KB可以将使用等价规则将每一个sentence转换为和取范式，然后再将和取范式转化为一个个全是析取的式子(DOL)组成一个新的KB',然后对于KB'中的DOL进行归结可以得到一个新的DOL，加入到KB'中。  

## 归结例子
![figure.3](https://gitee.com/zyp521/upload_image/raw/master/cHfQRp.png)

`$S={KB,\neg \alpha} $`, 我们称S为Resolution closure

**具体流程**:将alpha变为`$\neg \alpha $`然后加入到KB(通过语义等价转换为一个和取范式然后生成一个KB')中组成一个新的集合KB'，然后在这基础上进行归结, 由于归结是有限,总会有停止情况，如果最后能够归结出一个空子句则表示`$KB\models \alpha $`，对于上述的归结，每归结一次将生成的句子放到S中，然后直到停止之后，得到的就是RC(S)，如果要证明`$KB\models \alpha $`，则RC(S)中一定存在一个空语句。

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/xL4Mkd.png)

上述过程证明了规则是可靠(sound)的。  

S(是KB和`$\neg \alpha$`)是永假的，则表示不存在一个真值使得每一个sentences为真，若S为永假，则可以推出RC(S)中包含一个空语句。  

完备性可靠性得证。  

## A* Search
设计一个算法，任意给一个KB能否推出a。  
- 初始状态`${KB,\neg a}$`
- 找两个子句归结得到一个新的`${KB,\neg a,new sentences}$`（可以分成很多种情况，类似一个树划分为无数个节点）
- 然后进行继续划分节点搜索
- 直到首次到达终止状态

## Horn and Definite Clauses
- 正文字，负文字（带否符号的）  
- Defineite clauses: 很多个文字的析取，而且这些文字中有且仅有一个是正的
- Horn Clauses： 很多文字的析取，至多有一个正的，也可以全是负的
- 两个Horn Clauses进行归结得到的Clauses一定是一个Hron Clauses
- 析取为disjunction，合取为conjunction