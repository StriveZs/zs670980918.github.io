---
title: Learning In RNN Part I

categories:
  - 文章页
  - Python
  - Machine Learning
  - Neural NetWork

tags:
  - Python
  - Machine Learning
  - RNN
---

# Learning In RNN
**Recurrent Neural Network(RNN)** 
The chinese name is 循环神经网络.

## The introduction of RNN by Dr.Mofan Zhou

If you want some  dramatic explanations, please check here.[What is Recurrent Neural NetWorks?](https://www.youtube.com/watch?v=EEtf4kNsk7Q)
ps:If you don't have SSR, you can find the video in BiliBili.

For the input x(t), we can compute the Y(t) by RNN.

![figure1](https://gitee.com/zyp521/upload_image/raw/master/H7xlDk.png)

Then we can call the value S(t) that RNN compute.

![figure2](https://gitee.com/zyp521/upload_image/raw/master/7eJKIX.png)

Next RNN will compute the value in X(t+1) and get S(t+1). After that, Y(t+1) is equal S(t) add S(t+1).

![figure3](https://gitee.com/zyp521/upload_image/raw/master/4pNecb.png)

In generally, RNN is look like this:

![figure4](https://gitee.com/zyp521/upload_image/raw/master/deH7Ml.png)

 RNN has many structures and can do many things, like classification、regression and so on.
 
 ## The introduction by Dr.Hongyi Li
 The original video: [check here](https://www.youtube.com/watch?v=xCGidAeyS4M)
 
 ### Example Application
 #### Slot Filling(填槽)
 In many aspects in the life, we can use the slot filling, just like: intelligence customer service、ticket book system and so on.
 
 ![figure5](https://gitee.com/zyp521/upload_image/raw/master/MsmWaq.png)
 
 In this picture, we need the ticket book system can automatically slot the text in suitable loaction.
 
 ##### Solving slot filling by Feedforward network?
 **Net structure:**
 
 ![figure10](https://gitee.com/zyp521/upload_image/raw/master/UcqxoK.png)
 
 input: a ward (Each word is represented as a vector)
 
 output: Probability distribution(概率分布) that the input word belonging to the slots.
 
 ++If we can make our neural network have the ==memory==, so the network will classify if it is a destination or departure.++
 
==The way of make a word be represented as a vector==

**1-of-N encoding**

![figure7](https://gitee.com/zyp521/upload_image/raw/master/1LQDzw.png)

If we have n words, we can create a vector of length n. And each word will has a value equals one in different index.
 
**Beyond 1-of-N encoding**

If we have a word that not in our dictionary, we will classify it as other, So we must add a dimension for "other".

![figure8](https://gitee.com/zyp521/upload_image/raw/master/SlKJF2.png)

**Word hashing**
We can also use the word hashing to represent the word. We can make a letter vetcor.

![figure9](https://gitee.com/zyp521/upload_image/raw/master/Vz6XVL.png)

### Recurrent Neural NetWork
The output of hidden layer are stored in the memory.

![figure10](https://gitee.com/zyp521/upload_image/raw/master/i9WLXR.png)

#### Example

![figure11](https://gitee.com/zyp521/upload_image/raw/master/RSc0zS.png)

Presumed:

ALL the weights are "1", no bias.

All the activation functions are lienar.

Input sequence: `$ \left[ \begin{matrix}1\\1 \end{matrix} \right] \left[ \begin{matrix}1\\ 1 \end{matrix} \right] \left[ \begin{matrix}2 \\ 2 \end{matrix} \right] \dots \dots$`
 
 First, we must give the initial values of a. Default: 0
 
 **Step1:**
 
 ![figure12](https://gitee.com/zyp521/upload_image/raw/master/zsXfrl.png)
 
 Input 1 and 1, compute 0 and 1 will get the 2 and 2. And compute 2 and 2 will get 4 and 4. The first output will be 4 and 4, and the memory are 2 and 2.
 
 **Step2:**
 
 ![figure13](https://gitee.com/zyp521/upload_image/raw/master/lrOq8c.png)
 
 Input 1 and 1, compute 1 and 2 will get 6 and 6, And compute 6 and 6 will get 12 and 12. The second output will be 12 and 12, and the memory are 6 and 6.
 
 **Step3:**
 
 ![figure14](https://gitee.com/zyp521/upload_image/raw/master/4aDfln.png)
 
 Input 2 and 2, compute 2 and 6 will get 16 and 16, And compute 16 and 16 will get 32 and 32. The second output will be 32 and 32, and the memory are 16 and 16.
 
### RNN
#### Ticket Book System apply in RNN
**Step1:**

![figure15](https://gitee.com/zyp521/upload_image/raw/master/WBXdFc.png)

In the figure, arrive is inputed as x1, compute a1 by RNN and store it.

**Step2:**

![figure16](https://gitee.com/zyp521/upload_image/raw/master/ogz7xD.png)

In this figure, Taipei is inputed as x2, use x2 and a1 to compute a2 and store it.

**Step3:**

![figure17](https://gitee.com/zyp521/upload_image/raw/master/Wy8uKU.png)

In this figure, on is inputed as x3, use x3 and a2 to compute a 3 and store it.

**So on**

![figure18](https://gitee.com/zyp521/upload_image/raw/master/M9kqVh.png)

==Attention:== we are not have only one hidden layer. It can be so many.

#### Elman Network & Jordan Network
![figure19](https://gitee.com/zyp521/upload_image/raw/master/Kw2gPZ.png)

Elman Network we have talked above, and the Jordan Network is the new one we want to introduce.

Actually, the differnece between Jordan Network and Elman Network is that Jordan Network make the output to compute with next step computation.

#### Bidirectional(双向的) RNN
![figure20](https://gitee.com/zyp521/upload_image/raw/master/Iq4InB.png)

由上图所示，我们可以同时训练一个正向的循环神经网络，又可以训练一个逆向的神经网络，然后在将他们结果都输入到一个新的隐藏层进行计算产生`$ y^{t}\:\:\:y^{t+1}\:\:\:y^{y+2} \dots $`.

### Long Short-term Memory(LSTM)
![figure21](https://gitee.com/zyp521/upload_image/raw/master/R9BUka.png)

The LSTM has three gates, like input gate, forget gate, output gate.

For all gates, they have own neural network that can learning by themselves to decide how to control the Gate.

If the output of other part of the network want to input the memory cell, it must pass the input gate. And input gate also be controled by other part of the network. This action can study by itself, it can decide when to open the input gate.

By the way, the output gate and forget gate also have similar structure.

**Sepcial Neuron(特殊神经元):**
- 4 inputs
- 1 output

4 input:
- Other part of the network of Input Gate
- Signal control the input gate
- Signal control the output gate
- Signal control the forget gate

1 output:
- Other part of the network of Output Gate

++The LSTM can remember many memory cells in long time.++

#### Other expression

![figure21](https://gitee.com/zyp521/upload_image/raw/master/uMcAkq.png)

==Activation funcion f is usually a sigmoid function.==

The sigmoid function can support between 0 and 1. **0 stand for gate closed, 1 symbolic gate opened.** Mimic open and close gate.

![figure22](https://gitee.com/zyp521/upload_image/raw/master/cfRYnW.png)

`$ g(z)f(z_{i}) = g(z)\:multiply\: f(z_{i}) $`

`$ c\:multiply\:f(z_{f}) = cf(z_{f})$`

`$ c^{'}=g(z)g(z_{i})+cf(z_{f}) $`

`$ a = h(c')\:multiply\:f(z_{0}) $`

#### LSTM - Example

![figure23](https://gitee.com/zyp521/upload_image/raw/master/RrkPFk.png)

##### **Init:**
- one LSTM cell Memory
- 3 dimension input
- 1 dimension output

##### **Condition:**
- When `$ x_{2}=1$`, add the numbers of `$ x_{1} $` into the memory
- When `$ x_{2}=-1$`, reset the memory
- When `$ x_{3}=1 $`, output the number in the memory.

##### **Process:**

![figure24](https://gitee.com/zyp521/upload_image/raw/master/aBOGRx.png)

**step1:**

cell memory=0, `$ x_{1}=1\:\:x_{2}=0\:\:x_{3}=0$` 

**step2:**

cell memory=0，`$ x_{1}=3\:\:x_{2}=1\:\:x_{3}=0$`, because of `$ x_{2}=1 $` , add the numbers of `$ x_{1} $` into the cell memory.

**step3:**

cell memory=0, `$ x_{1}=2\:\:x_{2}=0\:\:x_{3}=0$`, no action

**step4:**

cell memory=3,`$ x_{1}=4\:\:x_{2}=1\:\:x_{3}=0$`,add the number of `$ x_{1}=4 $` into the memory(3+4=7)

**step5:**

cell memory=7,`$ x_{1}=2\:\:x_{2}=0\:\:x_{3}=0$`, no action


**step6:**

cell memory=7,`$ x_{1}=1\:\:x_{2}=0\:\:x_{3}=1$`, `$ x_{3}=1 $` output the number in the memory, y=7

**step7:**

cell memroy=7,`$ x_{1}=3\:\:x_{2}=-1\:\:x_{3}=0$`, `$ x_{2}=-1 $` reset the memory, make the cell memory equal 0

**step8:**

cell memmory=0,`$ x_{1}=6\:\:x_{2}=1\:\:x_{3}=0$`, `$ x_{2}=1$` add the number of `$ x_{1}$` into the memory, cell memory=6(0+6=6)

**step9:**

cell mempry=6,`$ x_{1}=1\:\:x_{2}=0\:\:x_{3}=1$`, `$ x_{3}=1 $` output the number in the memory, y=6

#### Other Example
![figure25](https://gitee.com/zyp521/upload_image/raw/master/Ngl75m.png)

##### Init
- four input
- one output
- cell memory=0
- every number of line represent weight

##### Process
**step1:**

for `$ x_{1}=3,x_{2}=1,x_{3}=0$`

Input=3×1+1×0+0×0+1×0=3

Input Gate=3×0+1×100+0×0+1×(-10)=90≈1

Forget Gate=3×0+1×100+0×0+1×10=110≈1

Output Gate=3×0+1×0+0×100+1×(-10)=-10≈0

Because outputgate=0 close the output gate, so y=0. And forget gate=1 add the number to cell memory, so cell memory=3.

![figure26](https://gitee.com/zyp521/upload_image/raw/master/JA1A62.png)

**step2:**

for `$ x_{1}=4,x_{2}=1,x_{3}=0$`

Input=4×1+1×0+0×1+1×0=4

Input Gate=4×0+1×100+0×0+1×(-10)=90≈1

Forget Gate=4×0+100×1+0×0+10×1=110≈1

Output Gate=4×0+1×0+100×0+1×(-10)=-10≈0

Because outputgate=0 close the output gate, so y=0. And forget gate=1 add the number to cell memory, so cell memory=7.

![figure27](https://gitee.com/zyp521/upload_image/raw/master/XaaX7E.png)

**step3:**

for `$ x_{1}=2,x_{2}=0,x_{3}=0$`

Input=2×1+0×0+0×1+1×0=2

Input Gate=2×0+0×100+0×0+1×(-10)=-10≈0

Forget Gate=2×0+100×0+0×0+10×1=10≈1

Output Gate=2×0+0×0+100×0+1×(-10)=-10≈0

Because inputgate gate=0 close the input gate,so input equal 0, outputgate=0 close the output gate, so y=0. And forget gate=1 add the number to cell memory, so cell memory=7.

![figure28](https://gitee.com/zyp521/upload_image/raw/master/TwEYUM.png)

**step4:**

for `$ x_{1}=1,x_{2}=0,x_{3}=1$`

Input=1×1+0×0+1×0+1×0=1

Input Gate=1×0+0×100+1×0+1×(-10)=-10≈0

Forget Gate=1×0+100×0+1×0+10×1=10≈1

Output Gate=1×0+0×0+100×1+1×(-10)=90≈1

Because inputgate gate=0 close the input gate,so input equal 0, outputgate=1 open the output gate, so y=7. And forget gate=1 add the number to cell memory, so cell memory=7.

![figure29](https://gitee.com/zyp521/upload_image/raw/master/WDb4wS.png)

#### Original NetWork
##### Simply replace the neurons with LSTM

![figure30](https://gitee.com/zyp521/upload_image/raw/master/iRUofA.png)

replace neurons: 

enter each group of x into the corresponding gate

4 time of parameters

![figure31](https://gitee.com/zyp521/upload_image/raw/master/tPL86E.png)

##### Comprehend cell memory deeply
![figure32](https://gitee.com/zyp521/upload_image/raw/master/DdnHMP.png)

Let `$ x^{t} $` multiply a vector to get `$ z^{f}\:\:z^{i}\:\:z\:\:z^{o}$`.

Each of them(`$ z^{f}\:\:z^{i}\:\:z\:\:z^{o}$`) to be used as input vector.
###### Simplify Structure
![figure33](https://gitee.com/zyp521/upload_image/raw/master/k4eGul.png)

![figure34](https://gitee.com/zyp521/upload_image/raw/master/801t0i.png)

![figure35](https://gitee.com/zyp521/upload_image/raw/master/TNudQf.png)

##### Multiple-layer LSTM
![figure36](https://gitee.com/zyp521/upload_image/raw/master/0STWjj.png)

This is quite standard now, and don't worry if you cannot understand this, Keras can handle it.(Kearas supports "LSTM","GRU","SimpleRNN" layers)


