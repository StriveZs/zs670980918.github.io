---
titile: 使用Google Colaboratory跑深度学习

categories:
  - 深度学习
  - 服务器

tags:
  - Google Colaboratory
  - PyTorch
  - Anaconda
  - GPU
---

# 使用Google Colaboratory跑深度学习
## 使用Colaboratory
首先，要使用Google的产品，翻墙是必须的吧。 然后点击进入Google云端硬盘，如下界面：  

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/8yyuL9.png)

然后点击新建--更多--Colaboratory,就会出现这个界面

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/VnpM8q.png)

红框可以修改页面名称，点击蓝框进行设置GPU运行

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/6F46Dw.png)

更改运行时的类型：

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/D6jwKw.png)

设置为GPU:

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/GA2mPH.png)

验证一下，输入如下代码运行：

```
import tensorflow as tf
tf.test.gpu_device_name()
```

出现如下结果则表示是GPU运行：

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/xq4iij.png)

可以使用如下命令查看cpu类型和CUDA 版本(方便安装pytorch用)

```
!/opt/bin/nvidia-smi
```

![figure.7](https://gitee.com/zyp521/upload_image/raw/master/pMg1We.png)

## 安装Miniconda3
这里提前说一下在Colaboratory的问题：  
就是在这个类似命令行的页面端无法进行conda虚拟环境的创建，只能使用base，而且需要特殊的方式来对conda进行使用。  


先使用命令行下载Miniconda3的sh安装包：

```
!wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

安装权限配置：

```
!chmod +x Miniconda3-latest-Linux-x86_64.sh
```

安装到指定位置，这里建议安装在/root/

```
!bash ./Miniconda3-latest-Linux-x86_64.sh -b -f /root/
```

激活conda:

```
!source /root/miniconda3/bin/activate
```

使用命令将conda配置成默认的命令行使用。 

```
!conda init
```



## 安装PyTorch
这里试过进行env的创建，但是创建成功之后无法进行命令行的切换，因此这里就直接在base上进行了。

安装pytorch，这里去pytorch官网选择对应的版本进行安装：

![figure.8](https://gitee.com/zyp521/upload_image/raw/master/5y3Ekz.png)

```
!conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
```

使用命令查看conda env：

```
!conda info --env
```

![figure.9](https://gitee.com/zyp521/upload_image/raw/master/SV6aZQ.png)

### 验证pytorch是否能够使用
首先直接编写代码进行验证能否直接使用自己安装的conda python:

```
import torch
print(torch.version)
```

![figure.10](https://gitee.com/zyp521/upload_image/raw/master/bsKyn8.png)

可以看到这里的python版本为3.6，和我们的版本不一样，我认为直接使用python编译的是用的自带的python。  

因此这里创建一个test.py文件上传上去，代码为:

```
import torch
print(torch.version)
```

然后使用命令行再次运行代码：

```
!python /content/test.py
```

结果为:

![figure.11](https://gitee.com/zyp521/upload_image/raw/master/7fpucU.png)

可以看出我们的python为3.8版本了，因此成功了。

## 安装MMDetection
### 安装mmcv
```
git clone https://github.com/open-mmlab/mmcv.git
cd mmcv
pip install /content/mmcv/.
```

![figure.12](https://gitee.com/zyp521/upload_image/raw/master/cGUR6D.png)

### 安装cpython等需求包

```
https://gitee.com/zyp521/upload_image/raw/master/cGUR6D.png
```

### 安装mmdetection
官方文档的安装方法：

```
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -r requirements/build.txt
pip install "git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI"
pip install -v -e . # or "python setup.py develop"
```

![figure.13](https://gitee.com/zyp521/upload_image/raw/master/ZT0X2A.png)

到此，我们就完成了mmdetection及其依赖库的安装。

有一个比较大的缺陷需要声明一下，就是如果你超过12小时不登录Colaboratory的话，google会自动将你的服务器重置分配给别人，你的数据和代码都被自动清楚了。
