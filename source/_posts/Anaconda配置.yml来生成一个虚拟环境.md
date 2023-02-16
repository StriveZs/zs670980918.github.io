---
title: Anaconda配置.yml来生成一个虚拟环境

categories:
  - Anaconda

tags:
  - Anaconda
  - Python
  - yml
  - conda
---

# Anaconda配置.yml来生成一个虚拟环境
创建新的环境的命令如下:
```
conda env create -f environment.yml
```
其中.yml是需要自己的配置的。

配置格式如下:
```
name: 虚拟环境名
channels:
  - pytorch
  - defaults
  - 还是使用国内地清华源、科大源等
dependencies:
  - 包名=版本号
  - pip:(使用pip 进行安装的一些包)
    - 包名=版本号
```

例子：
```
name: Total3D
channels:
  - pytorch
  - defaults
dependencies:
  - _libgcc_mutex=0.1
  - blas=1.0
  - pip:
    - cycler==0.10.0
    - jellyfish==0.8.2
```