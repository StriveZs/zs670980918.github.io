---
title: 环境配置：NVIDIA+Anaconda+PyTorch+PyCharm

categories:
  - Knowledge
  - PyTorch

tags:
  - NVIDIA
  - PyTorch
  - PyCharm
  - CUDA
---

# 环境配置：NVIDIA+Anaconda+PyTorch+PyCharm
## 步骤
### 配置英伟达显卡
#### 安装CUDA
- 首先打开自己的英伟达控制面板查看自己的系统信息，如下图所示：我的是CUDA10.2.95因此需要去英伟达官网下载对应版本的CUDA，下载地址：[click here](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork)

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/rr74XI.png)

![figure.0](https://gitee.com/zyp521/upload_image/raw/master/r1wfSH.png)
- 进行安装，基本上就是傻瓜式下一步没什么，等待安装完成即可

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/QNrK0e.png)

#### 安装Cudnn
- 首先去英伟达官网下载cudnn(这里需要登录下载)。具体下载链接：[click here](https://developer.nvidia.com/cudnn)
- 下载完成之后解压得到一个文件夹(蜜汁感动竟然是压缩包不用安装), 将文件夹中的内容放到在C盘路径为**C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\**的对应文件夹中，直接复制进去就好了

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/PRdOlQ.png)

### 配置PyTorch
- 这里我使用的是anaconda来进行包的管理，具体anaconda下载地址： [click here](https://www.anaconda.com/)
- PyTorch安装，**切记这里需要安装和cuda对应版本的PyTorch！**
- 首先去PyTorch官网找到安装命令，如下图：

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/AxTd0k.png)

- 然后在Anaconda中输入该命令即可：

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/PnvbJp.png)

- 安装完成

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/dUyIVX.png)

## 验证
### 版本验证
- 在命令行中输入
```
nvcc -V
```
会观察到如下版本信息：

![figure.7](https://gitee.com/zyp521/upload_image/raw/master/4ARnMy.png)

### PyCharm验证能够使用CUDA

```
import torch

print(torch.__version__)
print(torch.version.cuda)
print(torch.cuda.is_available())
```

如果输出结果为True，则表示cuda可以使用了。（建议不用最新版的NVIDIA驱动，否则CUDA版本也会升级 PyTorch不一定会有对应版本 没有对应版本不能正常使用。）