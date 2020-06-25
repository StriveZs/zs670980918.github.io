---
title: PyTorch中nn.Linear()理解

categories:
  - PyTorch
  - Python

tags:
  - Pytorch
  - Python
  - Linear
---

# PyTorch中nn.Linear()理解
## 计算公式
`$ y = xA^{T}+b$`

这里A为weight，b为bias。

## 代码部分
### 初始化部分代码
```
class Linear(Module):
	...
	__constants__ = ['bias']
	
	def __init__(self, in_features, out_features, bias=True):
	    super(Linear, self).__init__()
	    self.in_features = in_features
	    self.out_features = out_features
	    self.weight = Parameter(torch.Tensor(out_features, in_features))
	    if bias:
	        self.bias = Parameter(torch.Tensor(out_features))
	    else:
	        self.register_parameter('bias', None)
	    self.reset_parameters()
```

### 计算部分
```
@weak_script_method
    def forward(self, input):
        return F.linear(input, self.weight, self.bias)

```

返回值为: input * weight + bias

### bias和weight
```
weight: the learnable weights of the module of shape
    :math:`(\text{out\_features}, \text{in\_features})`. The values are
    initialized from :math:`\mathcal{U}(-\sqrt{k}, \sqrt{k})`, where
    :math:`k = \frac{1}{\text{in\_features}}`
bias:   the learnable bias of the module of shape :math:`(\text{out\_features})`.
        If :attr:`bias` is ``True``, the values are initialized from
        :math:`\mathcal{U}(-\sqrt{k}, \sqrt{k})` where
        :math:`k = \frac{1}{\text{in\_features}}`
```

## 示例
```
>>> import torch
>>> nn1 = torch.nn.Linear(100, 50)
>>> input1 = torch.randn(140, 100)
>>> output1 = nn1(input1)
>>> output1.size()
torch.Size([140, 50])
```

对于上述描述，我们创建一个input的维度为[140,100], 通过声明线性层会得到根据维度初始化的权重和偏差，其中weight的维度为[50,100]。对于公式中A表示的就是weight，而b表示的就是bias。由于对A进行了转置所以这里weight的维度为[50,100]而不是[100,50]。

具体计算为[140,100] × [50,100]的转置 + bias = [140,100] × [100,50] + bias最后得到的维度为[140,50]。

至于对于bias和weight的初始化，根绝网上所讲的是来有关维度值得均匀分布。