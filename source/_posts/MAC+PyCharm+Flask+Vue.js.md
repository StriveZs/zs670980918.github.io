---
title: MAC+PyCharm+Flask+Vue.js

categories:
  - MAC
  - Python
  - JavaScript

tags:
  - MAC
  - Python
  - PyCharm
  - Flask
  - Vue
  - JavaScript
---

# MAC+PyCharm+Flask+Vue.js
## 配置node.js+nvm+npm
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
nvm install 15.3.0
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
nvm use 15.3.0
```

可以使用如下命令查看当前node版本
```
node -v
```

### npm切换淘宝镜像
#### 临时的
临时使用的命令:
```
npm --registry https://registry.npm.taobao.org install express
```
#### 长久的
通过如下面命令：
```
npm config set registry https://registry.npm.taobao.org
```
配置完成之后，可以使用如下命令来得到当前的配置。
```
npm config get registry
```

## 安装Vue.js
这里我在我的node.js=15.3.0进行安装vue.js。  

安装vue-cli脚手架构建工具:
```
npm install -g @vue-cli
npm install -g @vue/cli-init
```
在安装好输入如下命令验证是否成功:
```
vue --version // 如果有版本号，则证明安装成功了
```

安装webpack:
```
npm install -g webpack
```

## 创建并运行Vue.js项目
### 在线初始化
使用cd命令进入项目目录，然后使用如下命令来初始化项目(下载template):
```
vue init webpack visProject
```

然后进入项目目录, 安装项目依赖得到node-modules目录:
```
npm install
```

### 离线方式
由于使用上述方式，一直显示在downloading template，这里使用的是webpack作为template，因此我考虑使用离线的方式进行初始化。  

首先先去下载webpack, 可以在gitee下载，下载链接:[click here](https://gitee.com/uyulnet/vuejs-templates-webpack)  
下载完成之后，在用户目录下面中的隐藏文件中找一下是否有.vue-templates文件夹，如果没有的话使用如下命令创建一个
```
mkdir .vue-templates
```
创建完成之后，将下载好的文件解压之后，改名成webpack，然后将文件夹放在该目录下。然后回到你之前的目录输入如下命令来离线初始化:
```
vue init webpack 项目名 --offline
```

初始化配置如下:

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/TR9kMI.png)

初始化之后使用如下命令，将当前执行环境添加到node_modules文件夹下:
```
npm install
```

### 运行项目
在完成上述配置之后，使用cd进入项目文件夹，使用如下命令来对项目进行编译:
```
npm run dev
```
编译完成之后, 就可以通过localhost来访问了。出现如下页面表示运行成功了.

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/2qh71D.png)

## src文件以及作用

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/4fuyhq.png)


### 解决打不开的问题
这里由于默认的我8080端口被占用了，因此可以通过修改配置文件，来给它分配新的端口来解决。
```
配置文件目录: ~/config/index.js

将里面dev一类下的port对应的端口号修改为8083即可.
```

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/Ewtcd9.png)

然后使用下面命令重新进行编译即可:
```
npm run dev
```

## 配置Flask
这里使用的IDE工具是：PyCharm，关于Python环境的搭建这里就不过多赘述了，网上有很多教程。  
### 安装Flask
使用如下命令安装flask库: 这里我使用的是Anaconda进行包管理。  
```
conda install flask
```

但是这里，我使用PyCharm创建一个新的项目的话，可以选择直接创建一个flask项目，选择如下:

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/EvhLHQ.png)

这样的话，是会自动在选择的解释器中安装flask的。

这里我使用的前者，因此我需要手动安装flask，安装完之后，使用PyCharm来创建一个新的Flask项目，如上图所示，创建完成之后，我们会得到如下内容:

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/lyOMJX.png)

运行app.py文件，我们可以通过访问[http://127.0.0.1:5000/](http://127.0.0.1:5000/)来得到一下界面。

![figure.7](https://gitee.com/zyp521/upload_image/raw/master/LzX4hb.png)

这表明我们配置完成了。综上我们分别配置好了vue和flask，后面会接着将如何使用。