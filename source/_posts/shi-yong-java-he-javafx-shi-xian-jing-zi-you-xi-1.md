---
title: 使用java和javafx实现井字游戏
url: 529.html
id: 529
categories:
  - Java
  - 小游戏
  - 文章页
date: 2018-04-06 17:17:03
tags:
  - Java
  - Game
---

![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406170916.png)

### javafx简介：

JavaFX是Oracle公司推出的图形和多媒体包，使开发人员能够设计、创建、测试、调试和部署富客户端应用程序，并在不同的平台上有致的运行效果。   相比于AWT，SWT, Swing等Java库，JavaFX的控件种类和UI效果都要好得多，且已经默认集成在最新的JDK包中。因此，开发人员只要安装了最新的JDK，就可以直接使用常用的开发工具如Eclipse开发JavaFX应用了。 新手学习开发JavaFX请参考Oracle的官方说明： [http://docs.oracle.com/javase/8/javafx/get-started-tutorial/](http://docs.oracle.com/javase/8/javafx/get-started-tutorial/)   这里我用javafx编写了图形界面的井字游戏： ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406171029.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406171102.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406171143.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406171203.png)   实际效果： ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180406171253.png)   其实这个还可以进行改进比如： 可以将X和O换成你想要得图片，Image就可以办到。 同样显示谁胜利还可以采用提示框，可以增添一个重新开局的按钮，以及计时器等等。   代码文件：[井字游戏 ](http://47.100.4.8/wp-content/uploads/2018/04/井字游戏.docx) 这里我将代码放到了word文档中。