---
title: Hexo中添加动态2d二次元人物模型

categories:
  - 文章页
  - Hexo
  - Next主题

tags:
  - 美化
  - hexo
  - next
  - 2D
  - 二次元
---

# Hexo中添加动态2d二次元人物模型

Hexo添加helper-live2d模型插件

[插件的github地址](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md)

插件作者提供了较为详细的安装步骤，我结合自己操作和图示，提供大家。

## 插件效果
![miku](https://gitee.com/zyp521/upload_image/raw/master/szEDae.png)

## 安装插件
hexo博客根目录使用git bash 输入以下代码，安装插件：
```
npm install --save hexo-helper-live2d
```

## 下载模型
作者提供以下模型的模型包，模型包预览地址见下面的链接，选择你想用的模型，记住名字，选择对应的后缀模型包

[作者各种模型包展示](https://github.com/xiazeyu/live2d-widget-models)

```

live2d-widget-model-chitose
live2d-widget-model-epsilon2_1
live2d-widget-model-gf
live2d-widget-model-haru/01 (use npm install --save live2d-widget-model-haru)
live2d-widget-model-haru/02 (use npm install --save live2d-widget-model-haru)
live2d-widget-model-haruto
live2d-widget-model-hibiki
live2d-widget-model-hijiki
live2d-widget-model-izumi
live2d-widget-model-koharu
live2d-widget-model-miku
live2d-widget-model-ni-j
live2d-widget-model-nico
live2d-widget-model-nietzsche
live2d-widget-model-nipsilon
live2d-widget-model-nito
live2d-widget-model-shizuku
live2d-widget-model-tororo
live2d-widget-model-tsumiki
live2d-widget-model-unitychan
live2d-widget-model-wanko
live2d-widget-model-z16
```

选择好对应的模型，使用 npm install 模型的包名来安装，比如我选择的的是live2d-widget-model-miku 模型包(大爱公主殿下)

## 配置
打开个人Hexo博客文件根目录下的 _config.yml 文件，在最后添加一下代码
```

live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-koharu
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
```

## 重启项目
输入
```
hexo clean && hexo g && hexo s
```