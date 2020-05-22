---
title: 使用百度 AI Studio来跑深度学习

categories:
  - Neural Network
  - Artificial Intelligence
  - Knowledge

tag:
  - Neural Network
  - Server
---

# 使用百度 AI Studio来跑深度学习
ps：这里不仅限于跑深度学习，可运行python代码。

具体网站:[click here](https://aistudio.baidu.com/)

**这里做完四个任务可以得到100小时的计算时长，同样每天运行项目可以得到12小时的计算时长！太香了~**

## 导入自己的项目
### 创建数据集
创建数据集并上传数据集压缩包（这里可用用别人开源的数据集）

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/Oc0r22.png)

### 创建项目
这里建议创建jupyter notebook的项目，因为他可以操控终端，这样就给了我们很多的可能，嘿嘿。

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/2qCy98.png)

直接启动环境打开终端，如果有计算时长可能选择高性能的tesla v100计算卡哦。

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/HWwpSU.png)

### 环境配置

在终端中输入如下命令可以查看显卡配置
```
NVIDIA-smi
```

如下：

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/123.png)

在终端输入如下命令，可以查看cuda版本。

```
nvcc -V
```

查看cuda环境配置，然后去PyTorch官方找到对应的pytorch版本进行命令行安装即可。

这样运行神经网络的基础配置就设置好了，

### 上传项目
进入项目后，点击上传按钮，将需要的代码文件上传到服务器即可。

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/UGMnEc.png)

## Final
最后这里特别说明一下，服务器的系统环境是linux内核，所以基本上各种数据集的解压（压缩包形式数据集）文件创建删除，代码的运行都是使用命令行来完成的。

将压缩包abc.rar 解压到指定路径
```
rar x abc.rar /home/aistudio/work/..../
```