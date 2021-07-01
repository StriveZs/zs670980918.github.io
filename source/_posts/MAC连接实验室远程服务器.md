---
title: MAC连接实验室远程服务器

categories:
  - 服务器
  - MAC

tags:
  - 服务器
  - MAC
---

# MAC连接实验室远程服务器
- 首先要确保路由器没有问题，因为我连别人的路由器就不能登陆，而自己的就可以

## 挂空天院专用VPN
- 首先打开系统偏好设置中的网络

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/MPuDkF.png)

- 创建VPN 选择L2TP

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/VVyMj1.png)

- 填写服务器地址和账户名

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/bOlkGK.png)

- 点击连接认证，设置密码和预设密钥

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/AOIdTM.png)

- 可以勾选上在菜单栏中显示VPN状态一栏，方面在桌面操作

## 使用终端访问服务器
使用如下命令:
```
ssh 用户名@主机地址 -p 端口号
```

然后提示要求输入密码之后，再输入密码就可以了。