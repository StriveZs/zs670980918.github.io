---
title: Cliclick 简单实用

categories:
  - 功能
  - Python

tags:
  - 鼠标单击
  - Python
  - Cliclick
---

# Cliclick 简单实用
好久没发东西，最近课程实在是太多了，太忙了。忙晕了害
最近需要用到模拟鼠标单击的东西，因此找了找感觉这个还可以简单易用，介绍一下。  

## 安装
### Homebrew
Homebrew包管理器 : brew install cliclick  

### 官网下载
也可以直接去官网下载安装包，进行下载安装包:  
[https://www.bluem.net/en/projects/cliclick/](https://www.bluem.net/en/projects/cliclick/)  

## 简单使用
打开终端，进入cliclick所在文件夹下，输入：

```
./cliclick -h
```
可以查看帮助。

### 打印当前鼠标的位置坐标
注意鼠标要事先放在你想要知道坐标的位置。  
```
./cliclick p
```

就可以得到一个坐标，

### 执行单击事件
```
./cliclick c:x,y 其中x和y分别为横坐标和纵坐标
```

在命令行输入该命令，鼠标就会自动平移过去执行单击事件了。

## 示例:
以下是我用python执行命令行来实现的固定位置的单击操作：，这样做的好处是可以重复的执行单击操作。

```
import os
import time

cmd1 = "./cliclick c:789,867"
cmd2 = "./cliclick c:669,792"
for i in range(1000):
    mess1 = os.system(cmd1)
    print(mess1)
    time.sleep(10)
    mess2 = os.system(cmd2)
    print(mess2)
    print('----' + str(i+1) + '------')
    time.sleep(100)
```