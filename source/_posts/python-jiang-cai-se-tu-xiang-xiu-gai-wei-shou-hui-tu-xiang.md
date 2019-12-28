---
title: Python将彩色图像修改为手绘图像
url: 460.html
id: 460
categories:
  - Python功能
  - python数据分析
  - 文章页
date: 2018-03-28 22:44:47
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/u407244128253124607fm27gp0-1-300x200.jpg) 这里是通过使用numpy.array数组来对图像进行处理。 这里是代码： ![](http://47.100.4.8/wp-content/uploads/2018/03/1231232132143425436457654.png) from PIL import Image import numpy as np a = np.array(Image.open("F:/a.png").convert('L')).astype('float') depth = 10. #（0-100） grad = np.gradient(a) #取图像灰度的梯度值 grad\_x,grad\_y = grad #分别取横纵图像的梯度值 grad\_x = grad\_x * depth / 100. grad\_y = grad\_y * depth / 100. A = np.sqrt(grad\_x\*\*2 + grad\_y\*\*2 + 1.) uni\_x = grad\_x / A uni\_y = grad\_y / A uni\_z = 1. / A vec\_e1 = np.pi / 2.2 #光源的俯视角度，弧度值 vec\_az = np.pi / 4 #光源的方位角度，弧度值 dx = np.cos(vec\_e1) * np.cos(vec\_az) #光源对x轴的影响 dy = np.cos(vec\_e1) * np.sin(vec\_az) #光源对y轴的影响 dz = np.sin(vec\_e1) #光源对z的影响 b = 255 * (dx * uni\_x + dy * uni\_y + dz * uni_z) #光源归一化 b = b.clip(0,255) im = Image.fromarray(b.astype('uint8')) #重构图像 im.save('F:/b.jpg')   原图： ![](http://47.100.4.8/wp-content/uploads/2018/03/546424323.png) 下面是效果图： ![](http://47.100.4.8/wp-content/uploads/2018/03/3242133123.png)