---
title: Windows下配置VSCode
url: 1827.html
id: 1827
categories:
  - VSCode
  - 文章页
  - 软件分享
date: 2019-04-17 19:46:00
tags:
---

**弄了很久总算搞好了，这里分享一下，QWQ** 一、软件安装 先去VSCode官网下载安装包 地址为：[https://code.visualstudio.com/Download](https://code.visualstudio.com/Download) 二、安装配置插件 先打开VSCode，打开扩展程序安装并安装如下插件： ![](http://47.100.4.8/wp-content/uploads/2019/04/1-1.png) 其中C/C++、C/C++ Clang和Code Runner是必备的，如果你需要中文版则可以安装Chinese language这个插件安装好后要重启以下VSCode 三、安装MinGW 首先如果没有codeblock或者DevC++的则可以考虑去官网下载MinGW的安装程序 网址为：[https://osdn.net/projects/mingw/releases/p15522](https://osdn.net/projects/mingw/releases/p15522) 具体安装过程详见：[https://blog.csdn.net/bat67/article/details/76095813](https://blog.csdn.net/bat67/article/details/76095813) 这里由于我已经安装过CodeBlock则不需要再次安装了，也就不过多的说了。 四、配置系统环境变量 如图操作即可，记得配置完环境变量要重启VSCode ![](http://47.100.4.8/wp-content/uploads/2019/04/2-1.png) 五、配置c\_cpp\_properties.json文件 首先要创建一个工作环境的文件夹，然后在这里面通过设置调出该文件，按照如下配置即可 ![](http://47.100.4.8/wp-content/uploads/2019/04/QQ图片20190417194139.png) 这里需要注意的是添加如下一行代码即可：

"E:/codeblock/CodeBlocks/MinGW/include/**"

添加完成之后在工作区创建一个Cpp文件使用运行即可。