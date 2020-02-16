---
title: Learning In RNN Part II

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

# Learning In RNN Part II
**Learning Tager:** Make the loss be minimize that evaluating by cost function.

![figure1](https://gitee.com/zyp521/upload_image/raw/master/kHcMXX.png)

## Unfortunately
- RNN-based network is not always easy to learn.

![figure2](https://gitee.com/zyp521/upload_image/raw/master/8bJy2V.png)

- Th error surface is rought

![figure3](https://gitee.com/zyp521/upload_image/raw/master/dy4doG.png)

## Helpful Techniques
### Long Short-term Memory(LSTM)
#### Why replace RNN to LSTM?
Can deal with gradient vanishing(消灭，等于0) (not gradient explode爆炸激增)  
It can make your error surface to be flatting nor not steep.  
The specify performance is that it can remove the flat regions and solve the problem of gradient vanishing, but not gradient explode.  
#### How to work:
The different operation between RNN and LSTM is that RNN can reomve value in memory after each computation and store new value. But LSTM can add the previous value to new value in cell memory after each computation.(Concretely depend on the value of forget gate)  
So the difference of RNN and LSTM is if a weight influence value of memory, the influence never disappears unless forget gate is closed.  
If forget gate is opened, there no gradient vanishing.  

#### Summarization
- can deal with gradient vanishing(not gradient explode)
- Memory and input are ++added++
- The influence never disappears
unless forget gate is closed
- No Gradient vanishing(If forget gate is opened)

Gated Recurrent Unit(GRU):simpier thant LSTM

**Other helpful techniques:**

![figure4](https://gitee.com/zyp521/upload_image/raw/master/EDrdli.png)  

## More Applications
### Many to one
- Input is a vector sequence, but output is only one vector.

**Sentiment Analysis:(意见分析)**

![figure5](https://gitee.com/zyp521/upload_image/raw/master/K5bxC0.png)

![figure6](https://gitee.com/zyp521/upload_image/raw/master/XKwMQM.png)

### Many to Many (Output is shorter)
- Both input and output are both sequences, **but the output is shorter**.

**Speech Recognition:**

![figure7](https://gitee.com/zyp521/upload_image/raw/master/QuBJ2j.png)

#### How to differentiate?
- Connectionist Temporal Classification(**CTC**，联结主义时间分类)

==Add an extra symbol "Φ" representing "null".==  

![figure8](https://gitee.com/zyp521/upload_image/raw/master/kCJIsg.png)

Use this method to slove the problem like differentiate "好棒" or "好棒棒".  
#### CTC Training
**Acoustic Features:(声音特征)**  
ALL possible alignments(序列/顺序) are considered as correct because we don't know what alignment is correct. So we can list all alignments to train.

![figure9](https://gitee.com/zyp521/upload_image/raw/master/WPPHRn.png)

#### CTC: example

![figure10](https://gitee.com/zyp521/upload_image/raw/master/3yexBF.png)

### Many to Many (No Limitation)
- Both input and output are both sequences **with differnet lengths**. ➡ **Sequence to sequence learning**  
**Machine Translate**(Machine Learning ➡ 机器学习)

**bag-of-word:**

![figure11](https://gitee.com/zyp521/upload_image/raw/master/HjyAMK.png)

Above model can't stop until it's interrupted.

#### How to make the network stop
- Adda a symbol '==='(断)

![figure12](https://gitee.com/zyp521/upload_image/raw/master/8Gu1j2.png)

### Beyond Sequence
- Syntactic parsing(句法分析)

#### Transform Tree Structure to sequence
**Conversion principle:**

![figure13](https://gitee.com/zyp521/upload_image/raw/master/BRp1UF.png)

We can transform sentence tree to sequence by using this principle and train a sequence model to recognize sentence.  

### Sequence-to-sequence
#### Auto-encoder-Text
- To understand the meaning of a word sequence, the order of the words can not be ignored.

![figure14](https://gitee.com/zyp521/upload_image/raw/master/By7XBu.png)

![figure15](https://gitee.com/zyp521/upload_image/raw/master/wYKkpA.png)

![figure16](https://gitee.com/zyp521/upload_image/raw/master/eCiGf3.png)

#### Auto-encoder-Speech
- Dimension reduction for a sequence with variable length

audio segments()word-level->Fixed-length vector  

![figure17](https://gitee.com/zyp521/upload_image/raw/master/RARIzh.png)

##### **Audio Search Principle:**

![figure18](https://gitee.com/zyp521/upload_image/raw/master/zYlxJy.png)

##### How to transform audio segment to vector

![figure19](https://gitee.com/zyp521/upload_image/raw/master/tTKbLU.png)

ps: jointly 共同地 同时地 similarity 相似 类似 embedding 埋入/埋葬  
##### Visualizing embedding vectors of the words

![figure20](https://gitee.com/zyp521/upload_image/raw/master/CGfD3r.png)

#### Sequence-to-sequence Learning Demo:Chat-bot

**Learning Principle:**

![figure21](https://gitee.com/zyp521/upload_image/raw/master/0szRES.png)

**Data Set:**  
40000 sentences in Movie album and discussion of presidential election in American.  

## Attention-based Model
**Structure Version 1:**

![figure22](https://gitee.com/zyp521/upload_image/raw/master/Ajbf8o.png)

**Structure Version 2:**  
==Neural Turing Machine(神经图灵机)==

![figure23](https://gitee.com/zyp521/upload_image/raw/master/h4FdpY.png)

### Reading Comprehension

![figure24](https://gitee.com/zyp521/upload_image/raw/master/ErGx83.png)

### Visual Question Answering

![figure25](https://gitee.com/zyp521/upload_image/raw/master/opnM0d.png)

**Principle:**  
==A vector for each region==

![figure26](https://gitee.com/zyp521/upload_image/raw/master/QyhNhJ.png)

### Speech Question Answering
- TOEFL Listening Comprehension Test By Machine

**Example:**  
1. Audio Story: the original story is 5 min long
2. Question: "what is possible of Venus' clouds?"
3. Choices:
   1. gased released as a result of volcanic activity
   2. chemical reactions caused by high surface temperatures
   3. bursts of radio energy from the plane's surface
   4. strong winds that blow dust into the atmosphere

#### Model Architecture
Everything is learned from training examples.

![figure27](https://gitee.com/zyp521/upload_image/raw/master/ADclLS.png)

## Deep & Structure
### Integrated together
- Speech Recognition: CNN/LSTM/DNN+HMM  
![figure28](https://gitee.com/zyp521/upload_image/raw/master/JKDhvu.jpg)

Bayes theorem

![figure29](https://gitee.com/zyp521/upload_image/raw/master/ssXaWg.png)

- Sematic Tagging: Bi-directional LSTM+CRF/Structured SVM  
Testing:  
![figure31](https://gitee.com/zyp521/upload_image/raw/master/zryrFy.jpg)

![figure30](https://gitee.com/zyp521/upload_image/raw/master/GJhyYd.png)
