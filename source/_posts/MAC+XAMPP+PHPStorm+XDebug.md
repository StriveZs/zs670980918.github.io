---
title: MAC+XAMPP+PHPStorm+XDebug

categories:
  - 文章页
  - PHP

tags:
  - PHP
  - PHPStorm
  - XAMPP
  - XDebug
---

# MAC+XAMPP+PHPStorm+XDebug
在网上找了半天，花费了很长时间，总结了网上的内容，发现写的都不是十分全面，这里我写了从头到尾的配置过程。

## 下载并安装XAMPP
首先先去官网下载：[click here](https://www.apachefriends.org/zh_cn/index.html)  

ps:个人补充一点，由于我上来先安装的是最新版本的导致我出现了许多问题，后来我尝试更换成了php7.3版本的XAMPP使用。

## 下载并安装PHPStorm
直接去官网下载并且安装即可，注意如果你不是教育版或者企业版，则需要购买或者使用密钥（自行查找吧）。 [click here](https://www.jetbrains.com/phpstorm/)

## 配置XAMPP
安装XMAPP之后，我们首先要配置一下conf文件.

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/U8PIJ1.png)

添加上你的端口，这里phpstorm默认使用的63342端口，因此我在配置文件中添加上了63342端口。

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/gEdJga.png)

修改成你想要的主站文件夹地址，由于它默认需要你将写好的文件放入到htdocs文件夹中，因此这里我为了方便自定义，我就修改了默认的主站地址。**注意这里写的内容将会成为你的localhost映射的地址**，在后面phpstorm项目配置的时候要注意，这里建议给一个比较大的文件范围作为默认的主站地址。

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/URpdu4.png)

如果没有权限的话，则将User 改成你自己的用户名即可。

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/IiOE3f.png)

按照上述过程配置好之后，重启以下apache就可以监听对应端口了。至于MySQL的我暂时没有到放在以后去写了。

## PHPStorm配置
首先是创建一个PHP项目，然后打开Preferences->Debugger设置一下端口号，这里我们直接使用的默认63342的，如果你不使用默认的话，这里修改了对应着conf配置文件也要修改。

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/Ql0vJT.png)

然后打开Deployment设置部署事宜。  

创建一个local or mounted folder，然后设置一下项目地址，以及启动的网站，这里如果不是默认80端口的话，都要添加上自己端口号。

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/POJUXS.png)

点开映射部分，设置一下自己的映射，**注意这里之前在conf文件夹中设置了父级主站目录**，因此我们需要在Web Path一栏中设置一下详细的目录，并且在local path中添加上项目地址。具体如下：

![figure.7](https://gitee.com/zyp521/upload_image/raw/master/4DEfk5.png)

配置完成之后一定要点一下那个小对勾，将该服务器设置为默认服务器。

![figure.8](https://gitee.com/zyp521/upload_image/raw/master/DdckXH.png)

## 配置PHP
注意如果你是mac系统的话，则不需要使用xampp的php，可以直接使用你mac自导的php，在终端输入php-version可以查看当前php的版本，然后你打开Preferences->-> Language -> PHP 来选择你的解释器，默认是没有选择的。

![figure.9](https://gitee.com/zyp521/upload_image/raw/master/mNJ27O.png)

注意两个栏的版本要一直，如果想要使用xampp中的php，则新建一个php，然后找到XAMPP/xamppfiles/bin/php-7.3.17来创建一个新的php。

![figure.13](https://gitee.com/zyp521/upload_image/raw/master/SQdQUu.png)

## 配置XDebug
### 安装xdebug扩展
- 查询与当前环境匹配的 xdebug 版本 [click here](https://xdebug.org/wizard)
- 进入bin文件夹，cd /Applications/XAMPP/bin
- sudo ./pecl search xdebug-2.x.x 这里的版本号根据上面查找到的
- sudo ./pecl install xdebug-2.x.x  安装
- 在etc文件夹中找到php.ini的最后添加如下内容
```
zend_extension=/Applications/XAMPP/xamppfiles/lib/php/extensions/no-debug-non-zts-20180731/xdebug.so ;该行内容在安装完 xdebug 后，可从安装结束语中获取
xdebug.remote_enable = 1
xdebug.remote_host = 127.0.0.1
xdebug.remote_port = 9000
xdebug.idekey = PHPSTORM
xdebug.auto_start = 1
```
- 重启apache服务器

### 配置PHP
打开Perference->Language->Debuger, 设置端口号为9000

![figure.13](https://gitee.com/zyp521/upload_image/raw/master/fz3haO.png)

打开Perference->Language->Debuger->DBGp Proxy 配置代理信息

![figure.14](https://gitee.com/zyp521/upload_image/raw/master/dlnNw2.png)

配置Server

![figure.15](https://gitee.com/zyp521/upload_image/raw/master/fFrJL9.png)

创建PHP Web并进行配置

![figure.16](https://gitee.com/zyp521/upload_image/raw/master/4uL0fc.png)

### 安装Chrome插件
安装Chrome xdebug 插件，并且配置为debug模式 [click here](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?utm_source=chrome-ntp-icon)

### PHPSTORM开启监听
绿色小电话！！！

![figure.17](https://gitee.com/zyp521/upload_image/raw/master/t2AJ2X.png)

## 运行
当你配置完成之后，创建一个php文件。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>id</title>
</head>
<body>
<?php
 echo "hello world";
?>
</body>
</html>
```

单击chrome运行即可以在浏览器中查看项目。

![figure.10](https://gitee.com/zyp521/upload_image/raw/master/ENYizv.png)

![figure.11](https://gitee.com/zyp521/upload_image/raw/master/HSYcz5.png)

ps：补充一年，如果你想设置运行按钮单击直接显示网页的话，则添加一个PHP Web Page

![figure.12](https://gitee.com/zyp521/upload_image/raw/master/yCmBS9.png)