---
title: MAC安装Cesium环境

categories:
  - MAC
  - Cesium

tags:
  - MAC
  - Cesium
---

# MAC安装Cesium环境
## 配置NodeJs+nvm+npm
访问github官方地址，根据官方的文档来安装Mac版本的nvm，[click here](https://github.com/nvm-sh/nvm)

这里建议用[nvm](https://github.com/nvm-sh/nvm)安装管理Node.js

**cURL:**
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```
**Wget:**
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```
nvm安装好后，重启终端，然后安装Node.js：
```
nvm ls-remote
```
使用上述命令来查看远程node版本，然后根据需要安装最新版本的Nodejs：
```
nvm install 10.15.1
```

安装完成之后可以使用
```
nvm list
```
来查看已经安装的nodejs版本，并且使用
```
nvm use 版本号
```
来使用对应版本的nodejs。

```
nvm use 10.15.1
```

可以使用如下命令查看当前node版本
```
node -v
```

我最新版本的NodeJs报错，这里就是使用10.15.1版本的NodeJs

### NodeJs卸载
首先使用nvm的命令停止活跃的NodeJs
```
nvm deactivate
```

然后使用下面命令下载对应版本的NodeJs
```
nvm uninstall xxx版本号
```

## 安装cesium
访问Cesium官方网站，[click here](https://cesium.com/downloads/)，使用如下命令安装最新版本的Cesium

```
npm install cesium
```

另外一种办法是去官方下载CesiumJs，这里我采用的是去官方下载。
下载完成之后进入到对应的目录中执行下面安装命令:

```
cd ~/Cesium-1.80
npm install
```

## 运行Cesium
安装完成之后，会在Cesium文件夹中生成一个node_moudles文件夹。如下所示是:

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/Gdg5sO.png)


然后运行执行下面命令运行cesium服务。

```
①：npm start
②：node servcer.cjs
```

然后访问[Connect to http://localhost:8080/](http://localhost:8080/)
出现下述界面则表示成功了：

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/OGMzZZ.png)

也可以访问Demo界面(HelloWorld):[http://localhost:8383/Apps/HelloWorld.html](http://localhost:8383/Apps/HelloWorld.html)

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/BGTark.png)

两个关键的网址:
- [http://localhost:8383/Build/Documentation/index.html](http://localhost:8383/Build/Documentation/index.html)  这是所有API说明文档
  - 某一个模块的所有函数，属性
  - 部分效果截图
  - 部分函数，属性调用代码示例
- [http://localhost:8383/Apps/Sandcastle/index.html](http://localhost:8383/Apps/Sandcastle/index.html)  这是沙盒
  - 可以浏览当前版本的一些功能特性
  - 一个可运行的代码库
  - 新建一个页面用于代码测试
  - 导出测试代码

## 比较好的学习方式
- (1)先浏览一遍沙盒的所有示例，Cesium能做什么，能做成什么样
- (2)做自己需要的功能时，查找到相关示例的代码，最好是看看深层次代码
- (3)如果时进行深层次的研究，则需要对WebGLass有更新层次的了解
- (4)用它做自己感兴趣的项目

## 问题整理
这里注意一下，如果你使用默认的8080端口，出现访问失败的情况，可能是你的端口号被占用了，可以使用mac命令来杀死端口号，但是这里我建议修改成其他的端口号来进行访问即可。

修改目录中的server.cjs文件

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/O2yuiN.png)

这里我用的是8383