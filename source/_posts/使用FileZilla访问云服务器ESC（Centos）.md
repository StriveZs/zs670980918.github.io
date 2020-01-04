---
title: 使用FileZilla通过sftp连接以Linux为内核的云服务器
categories:
 - 文章页
 - 服务器
 - Linux
tags:
 - 服务器
 - Linux 
---
# 使用FileZilla通过sftp连接以Linux为内核的云服务器
## 首先去FileZilla下载该软件进行安装
下载地址：https://filezilla-project.org/
## 登陆阿里云实例控制台
### 创建新的安全组规则
打开端口22
![规则](https://gitee.com/zyp521/upload_image/raw/master/NzEVB8.png)
### 使用VNC连接使用终端
连接VNC需要输入连接密码，这个是在购买阿里云服务器是已经给的。
![VNC](https://gitee.com/zyp521/upload_image/raw/master/TPs1tL.png)
### 配置ssh文件
进入ssh文件夹
```
cd /etc/ssh
ls
```
### 使用vim编辑sshd_config文件
```
vim sshd_config
```
**特别注意：** 使用配置该文件时需要选择e模式，然后如果在网页上显示不全的话建议使用一个更大的屏幕去操作，这样方便去看提示。

### 将配置添加到配置文件中
==配置代码==
```
##注释掉这一行

#Subsystem sftp/usr/libexec/openssh/sftp-server

##修改为

Subsystem sftp internal-sftp  ##指定sftp服务使用系统自带的internal-sftp

Match Group sftp  ##匹配sftp组的用户

ChrootDirectory /data ##sftp主目录指定到/data

ForceCommand internal-sftp  ##指定sftp命令

AllowTcpForwarding no   ##用户不能使用端口转发

X11Forwarding no  ##用户不能使用端口转发
```
==一定要注意== 将该配置添加到sshd_config文件最后，由于我之前添加到了UseDNS那一行的前面，导致ssh一直报错。

对于ssh报错可以使用如下命令调试：
```
ssh -t
```
得到问题描述之后一次去解决就好了。

配置完成之后退出并且保存文件。

### 重启ssh服务
在终端输如下命令来重启ssh服务：
```
service sshd restart
```

以上就大功告成了，下面只需要通过FileZilla来连接即可。
## 使用FileZilla连接
![filezilla](https://gitee.com/zyp521/upload_image/raw/master/3vyTxz.png)
用户名和密码都是在购买云服务器时提供的ftp密码。

主机为你的公网ip地址，输入完成之后点击快速连接即可。