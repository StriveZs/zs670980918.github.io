---
title: 将域名从服务器解析到github page上

categories:
  - 文章页
  - Github
  - 域名

tags:
  - 域名解析
  - Github Page
---
# 将域名从服务器解析到github page上
1. 首先停用掉自己之前的所使用的的子域名

![figure1](https://gitee.com/zyp521/upload_image/raw/master/n2rrTi.png)

2. 然后将列表中关于服务器解析的相关记录去除掉防止出现冲突

![figure2](https://gitee.com/zyp521/upload_image/raw/master/JzKtQB.png)

3. 然后修改github上项目配置将著名设置为++www.stirvezs.com++.

![figure3](https://gitee.com/zyp521/upload_image/raw/master/jnIjhS.png)

4. 修改hexo中的配置文件将url：改为www.strivezs.com

![figure4](https://gitee.com/zyp521/upload_image/raw/master/5cew7x.png)

5. 在域名管理里面添加域名解析
主机记录：www 用于www.strivezs.com的访问  
主机记录：@ 用于strivezs.com的访问

![figure5](https://gitee.com/zyp521/upload_image/raw/master/LdTBEN.png)

6. 使用hexo c&&hexo g && hexo d将项目重新部署到github上即可。