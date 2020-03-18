---
title: 使用CDN加速github page访问

categories:
  - 文章页
  - Github
  - 域名

tags:
  - 域名解析
  - Github Page
  - CDN加速
---

# 使用CDN加速github page访问
这里我使用的[七牛云](https://portal.qiniu.com/)来加速网站的访问.

**特别注意：你的域名一定要备案了才能用CDN！！！**

## 步骤
### 创建CDN域名加速实例
![figure1](https://gitee.com/zyp521/upload_image/raw/master/099ePA.png)

### 配置实例

![figure2](https://gitee.com/zyp521/upload_image/raw/master/MNex84.png)

![figure3](https://gitee.com/zyp521/upload_image/raw/master/m4lIay.png)

配置完如上实例后，需要等待实例状态变为成功:

![figure4](https://gitee.com/zyp521/upload_image/raw/master/XbWs3j.png)

### 添加到CNAME解析
打开你自己的域名管理控制台。这里我用的是阿里云的域名管理控制台，进行域名就解析的配置：

#### 配置www

![figure5](https://gitee.com/zyp521/upload_image/raw/master/LnLHLc.png)

#### 配置@

![figure6](https://gitee.com/zyp521/upload_image/raw/master/opB6nc.png)

## 验证解析成功没有
### mac/linux
在命令台输入
```
dig 你的网址
```

如果返回如下结果则表明解释成功了.

![figure7](https://gitee.com/zyp521/upload_image/raw/master/eI5g8q.png)
### Windows
由于这里我是mac系统所以windows我就贴出网上找到的验证方式：

windows系统可以通过Win+R 或 点击左下角的“开始”按钮打开“开始”菜单，打开“运行”，输入cmd回车。

在命令行模式下输入nslookup 您的加速域名，例如 nslookup qn.vinchi.club,在结果中可以看到您复制的cname值即可

![figure8](https://gitee.com/zyp521/upload_image/raw/master/Uz6PkK.jpg)