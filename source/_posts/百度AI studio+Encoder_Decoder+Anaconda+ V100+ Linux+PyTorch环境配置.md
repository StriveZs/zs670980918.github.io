---
title: 百度AI studio+Encoder_Decoder+Anaconda+ V100+ Linux+PyTorch环境配置

categories:
  - Knowledge
  - 毕设
  - Linux

tag:
  - Linux
  - Anaconda
---

# 百度AI studio+Encoder_Decoder+Anaconda+ V100+ Linux+PyTorch环境配置
这里主要以我的毕设代码需要的环境进行配置的，该内容配合miniconda可以扩展到其他的环境下。

## 环境配置
### dataset存储
由于在百度AI Studio中每次项目终止后，data数据集文件夹会按照数据集中的内容重置，因此我需要将需要的数据自行解压到work文件夹下，这样需要的内容就可以保存下载来了。具体解压代码：
```
rar x abc.rar /home/aistudio/work/..../
```

### Miniconda
**问题**：由于我之前直接在linux下的python进行pytorch的安装，这种情况只能在项目未关闭的情况下使用，但是当我第二天重启之后发现自动重置了，我之前安装的没了，因此下面我重新装了一个miniconda进行包管理，这样在下次重启之后不会被重置了。

#### 安装miniconda及其配置
```
下载：
wget -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh
安装：
bash Miniconda3-4.7.12.1-Linux-x86_64.sh

激活conda：
source ~/miniconda3/bin/avtivate

更换清华源：
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ 
conda config --set show_channel_urls yes
```
完成上述操作后，重启一下终端

#### 配置PyTorch环境
创建conda新环境并且配置需要的包
```
激活conda
source ~/miniconda3/bin/activate

创建环境
conda create --name Env_PyTorch python=3.7

进入创建好的环境
conda activate Env_Pytoch

安装PyTorch
conda install pytorch==1.2.0 torchvision==0.4.0 cudatoolkit=9.2
(去除掉-c pytorch才是使用清华源进行安装的否则仍然是原有的源安装)

配置其他的需要的包
conda install ipython
conda install scikit-image
conda install scipy==1.2.0
conda install tqdm
conda install pillow=6.1
conda install h5py
conda install nltk
```
#### 验证是否安装PyTorch成功
```
python
>>>import torch >>>print(torch.cuda.is_available()) 
>>>print(torch.__version__)
```

**注意**：每次重启终端都要重新运行
```
source ~/work/miniconda3/bin/activate 
conda activate Env_PyTorch
```

## 常见问题
我想把本地项目文件上传至Notebook项目中, 但文件数量比较多, 怎么上传? （详见官方帮助文档） 
- 请将项目文件打成zip包后, 在Notebook环境中上传. 如果项目文件较大(>30mb), 请使用数据集功能上传, 然后挂载到项目中.
- 最后在项目中通过unzip命令进行解压缩(请注意需要解压到work目录下)
如：将压缩文件text.zip在指定目录/tmp下解压缩，如果已有相同的文件存在，要求unzip命令不覆盖原 先的文件。
```
unzip -n test.zip -d /tmp
```
- 如执意需要.rar包, 由于该格式为RAR共享软件独有
使用如下语句：
```
rar 即可得到命令格式和所有参数
rar x abc.rar /home/aistudio/work/..../
```