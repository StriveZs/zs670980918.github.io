---
title: Focal Loss

categories:
  - Loss
  - DL

tags:
  - Focal Loss

mathjax: true
---

# Focal Loss
## 介绍
本质上讲，Focal Loss就是一个解决**分类问题中类别不平衡、分类难度差异**的一个Loss。该损失函数降低了大量的简单的负样本在训练中所占的权重。  

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/CycFSY.jpg)

CE为交叉熵Loss，而FL为Focal Loss

## Focal Loss——二分类
Focal Loss的形式(没有引入权值`$\alpha$` )是:  

$$L_{fl}=\left\{\begin{matrix}-(1-\hat{y})^{\gamma}log\: \hat{y},y=1 \\ -\hat{y}^{\gamma}log\:(1-\hat{y}),y=0 \end{matrix}\right.$$

对于该式子 `$\hat{y}$`为预测值，而y为真实标签, `$\gamma$`的作用就是调节权重曲线的陡度。  
`$L_{fl}$`实际上已经包含了对不均衡样本的解决办法，比如：负样本远比正样本多时，模型肯定会倾向于样本数目多的负类，这是如果负类的`$\hat{y}^{\gamma}$`比较小，而正类的`$(1-\hat{y})^{\gamma}$`比较大时，模型就会集中注意力关注正样本。  

我们已知`$1-\sigma(x)=\sigma(-x)$`且`$\hat{y}=\sigma{x}$` 因此对上面的式子我们可以变换得到:  

`$ L_{fl}=\left\{\begin{matrix}-\sigma^{\gamma}(-x)log\:\sigma{x},y=1 \\ -\sigma^{\gamma}{x}log\:\sigma(-x),y=0 \end{matrix}\right. $`

同时，可以引入一个权重调整`$\alpha$`， 会对结果有微小的提升。  

`$ L_{fl}=\left\{\begin{matrix}-\alpha\sigma^{\gamma}(-x)log\:\sigma{x},y=1 \\ -(1-\alpha)\sigma^{\gamma}{x}log\:\sigma(-x),y=0 \end{matrix}\right. $`

在他的文章中，经过一系列调参得到了`$\alpha=0.25,\gamma=2$`对于他的模型来说效果是最好的。如果需要对需要对`$\alpha$`进行选择的话，需要使用大的训练样本和算力进行调参。如果要求不太高的话，可以把`$\alpha$`设置为0.5即可。  

简单说一下这里如果是我进行调参的话，我会使用控制变量法，设定一个`$\alpha$`的衰减系数，然后给定一个初始的参数值进行训练，每经过一次完整的训练则将这个α对应的准确率记录下来，经过n次衰减后，对比记录得到的结果进行参数alpha的选择。

## Focal Loss——多分类
Focal Loss在多分类的形式可以根据二分类的形式得到:  
`$ L_{fl}=-(1-\hat{y})^{\gamma}log\:\hat{y}_{t} $`

其中`$\hat{y}_{t}$`为目标的的预测值，一般这个值是经过softmax之后结果。  

如果我们引入权重值`$\alpha$`之后的样子是:  

`$ L_{fl}=-\alpha_{t}(1-\hat{y})^{\gamma}log\:\hat{y}_{t} $`

其中每个类别都有一个对应的`$\alpha_{t}$`，并且保证`$\sum_{t=1}^{n}\alpha_{t}=1$`, 即所有类别的α之和为1.