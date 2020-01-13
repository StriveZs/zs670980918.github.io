---
title: Anaconda`s problem of pip

categories:
  - 文章页
  - Python
  - Anaconda

tags:
  - Python
  - Anaconda
  - pip
---

# Anaconda`s problem of pip
## Anaconda安装pip
**步骤**
1. 在对应的环境中打开terminal
2. 输入conda install setuptools，安装相关的包下载工具
3. 然后输入 conda install pip 即可安装

## 给pip更换国内源
**步骤**
1. 使用windows+R打开运行
2. 输入%HOMEPATH%
3. 在用户目录文件夹下创建pip.ini用txt打开（如果有则直接打开）
4. 更换国内源
```
[global]
timeout = 10 # 设置超时，单位s
index-url =  http://mirrors.aliyun.com/pypi/simple/   # 指定优先下载源
extra-index-url= http://pypi.douban.com/simple/   # 第二下载源
[install]
trusted-host=
    mirrors.aliyun.com
    pypi.douban.com
```

## 解决SSL问题
在更换完国内源之后仍然出现SSL，连接失败问题的话，则给出下述办法。
**步骤**
1. 找到该地址**D:\Anaconda\pkgs\openssl-1.0.2p-hfa6e2cd_0\Library\bin**
2. 然后将它添加到User的系统环境变量中即可。