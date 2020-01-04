---
title: Hexo中适用于Next主题的评论功能Gitalk

categories:
  - 文章页
  - Hexo
  - Next主题

tags:
  - 美化
  - hexo
  - next
  - 评论
  - Gitalk
---

# Hexo中适用于Next主题的评论功能Gitalk

Gitalk 是一款基于 Github Issue 和 Preact 开发的评论插件，评论时需使用 Github 账号进行登录，另一款 Gitment 与之类似。这里记录下在 NexT 主题中集成 Gitalk 的相关步骤。

## 注册应用
可直接打开：https://github.com/settings/applications/new 进行注册（此操作需要登录）
1. 填写注册信息
![figure](https://gitee.com/zyp521/upload_image/raw/master/9TUhWA.png)
2. 参数详解
```
# 参数说明:

Application name： # 应用名称，随意填写

Homepage URL： # 网站URL，如 http://blog.strivezs.com/

Application description # 描述，随意填写

Authorization callback URL：# 网站URL，http://blog.strivezs.com/
```
3. 管理界面
![figure](https://gitee.com/zyp521/upload_image/raw/master/jEtsnW.png)

## 配置
### 创建gitalk.swig文件
定位到路径/themes/next/layout/_third-party/comments/，创建gitalk.swig文件，内容：
```
   {% if page.comments && theme.gitalk.enable %}
   <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
   <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
   <script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
   <script type="text/javascript">
        var gitalk = new Gitalk({
          clientID: '{{ theme.gitalk.ClientID }}',
          clientSecret: '{{ theme.gitalk.ClientSecret }}',
          repo: '{{ theme.gitalk.repo }}',
          owner: '{{ theme.gitalk.githubID }}',
          admin: ['{{ theme.gitalk.adminUser }}'],
          id: md5(window.location.pathname),
          distractionFreeMode: '{{ theme.gitalk.distractionFreeMode }}'
        })
        gitalk.render('gitalk-container')
       </script>
{% endif %}
```
### 引入gitalk.swig
在同级目录下的index.swig里面加入
```
{% include 'gitalk.swig' %}
```
### 修改comments.swig，添加gitalk
修改 /themes/next/layout/_partials/comments.swig，添加内容如下，与前面的elseif同一级别上:
```
{% elseif theme.gitalk.enable %}
 <div id="gitalk-container"></div>
```

### 新建gitalk.styl样式
定位到/themes/next/source/css/_common/components/third-party/然后创建gitalk.styl文件，内容如下：
```
.gt-header a, .gt-comments a, .gt-popup a
  border-bottom: none;
.gt-container .gt-popup .gt-action.is--active:before
  top: 0.7em;
```

### 引入gitalk.styl样式
然后在同级别的third-party.styl中导入:
```
@import "gitalk";
```

### 修改主题配置文件
在主题配置文件theme/next/_config.yml中添加如下内容:
```
# gitalk评论
gitalk:
  enable: true
  githubID: StriveZs
  repo: name.github.io
  ClientID: 4a8689xxxxxxxxde63c1
  ClientSecret: f21bbd96c4b9963086479xxxxxxx6d0f1e3936348
  adminUser: StriveZs
  distractionFreeMode: true

```
==说明==
```
githubID : 你的github ID，用来说明你是个人还是某个组织的；

repo : 你要新建一个repo来保存这些comments，这里repo就随便新建一个就行；

ClientID 和 ClientSecret : 就是文章开头新建APP的那些，请注意，这个一定要和你部署的网站的对应起来，一个网站对应一个这个client；

adminUser: 你的admin 用户名，通常就是你自己
```

以上就是NexT中添加gitalk评论的配置，博客上传到GitHub上后，打开页面进入某一博客内容下，就可看到评论处。