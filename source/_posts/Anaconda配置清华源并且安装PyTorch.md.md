# Anaconda配置清华源并且安装PyTorch
## 配置清华源
```
配置基础包：
conda config --add channels http://mirror.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels http://mirror.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

配置拓展包比如PyTorch
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/

执行：
conda config --set show_channel_urls yes
```

## 安装PyTorch
去官网选择对应的版本安装，**需要注意的是要去掉 -c pytorch 否则安装的源来自于官网而不是自己之前设置的源**

如下：

```
conda install pytorch torchvision cudatoolkit=9.0 -c pytorch
改为
conda install pytorch torchvision cudatoolkit=9.0
```

建议：在我们搭建好环境之后，最好就先添加镜像站到Anaconda中，这样安装包的时候，速度会得到大大的提升