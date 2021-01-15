---
title: Mac+Sublime+Latex+Skim配置latex编辑环境

categories:
  - MAC
  - LaTex

tags:
  - Sublime
  - Skim
  - Latex
  - MAC
---

# Sublime+Latex+Skim配置latex编辑环境
## 安装步骤
### 安装Sublime Text
首先需要安装Sublime Text 2/3和Package Control，这个有大把的帖子。  

### 安装MacTex
MacTex现在是一个2G+的大包子，其实里面很多东西我们不需要，所以本着节约精神，我们安装MacTex_Basic包就行了，现在的版本大概是100M以内。这个安装也是傻瓜的。  

### 配置
在Sublime Text里Command+Shift+P调出命令窗口，输入Install，之后选择LaTexTools，网络OK的话，很快就完成了插件安装。  

LaTexTools插件会在编译你的Tex文件后，调用Skim这个PDF阅读器打开编译出的PDF文件，因此你还需要安装Skim.  

#### 配置Skim
运行一下Skim，进入偏好设置——同步，在PDF-Tex同步支持那里选择自定义，输入 **/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl** 第二行不用动。这样，当你在Sublime Text里修改tex文件时，Skim预览也会相应变更。  

### 测试
完成上面所有步骤，其实就已经搭建完成基本环境。创建一个test.tex文档，保存一下以后，Sublime Text会自动套用LaTex语法显示和编译。贴上我后面附的测试代码，一般来说Command+B应该可能会报fontspec错误；如果能正常编译，则会调用Skim显示一个PDF文档了。只是中间的中文不见了。  

### 中文环境
让我们最后来修改编译和中文环境：
打开终端，运行：
```
sudo tlmgr update --self
sudo tlmgr install latexmk
```

在ST里打开LaTeXTools.sublime-settings（也就是LaTeXTools的用户设置    

如果你是从旧版本升级上来或者担心这个配置文件出现问题，可以依次点击Preferences——Package Settings——LaTeXTools——Reconfigure LaTeXTools and migrate settings重建配置文件），在builder-settings下面新增两项配置：
```
"program" : "xelatex",
"command" : ["latexmk", "-cd", "-e", "$pdflatex = 'xelatex -interaction=nonstopmode -synctex=1 %S %O'", "-f", "-pdf"],
```

另外注意之前应该有"builder": "default"（或直接设置为空或”traditional”）。


保存配置文件后关闭，重新编译一下，中文正常啦！

#### 简单的中文设置方法
仅需要将在tex文件前面添加上如下代码即可：

```
%!TEX program = xelatex
%!TEX TS-program = xelatex
%!TEX encoding = UTF-8 Unicode
```

以及添加 ctex包
```
\usepackage[UTF8]{ctex}
```

## 总结

LaTeXTools默认调用Skim来打开生成的PDF文件，如果你更喜欢使用OS X自带的“预览”，现在可以直接在用户设置中增加：
"viewer": "preview",
目前还不支持其他PDF工具。

附上我的配置文件：https://pan.baidu.com/s/1pKGYHfX 密码：b27u

测试代码
```
\documentclass{article}
\usepackage{xeCJK, fontspec, xunicode, xltxtra}  
\setCJKmainfont{Hiragino Sans GB}  

\title{Title}
\author{}

\begin{document}

\maketitle{}

\section{Introduction}

This is where you will write your content. 在这里写上内容。

\end{document}
```

LATEX的其他选择
如果觉得修改设置看起来很复杂，可以在每篇文档前增加%!TEX program = xelatex，这会强制使用xelatex，也是解决中文的一个方法。

如果只是偶尔需要输入公式，这里介绍一个在线的LaTex公式编辑器  [http://www.codecogs.com/latex/eqneditor.php](http://www.codecogs.com/latex/eqneditor.php)
