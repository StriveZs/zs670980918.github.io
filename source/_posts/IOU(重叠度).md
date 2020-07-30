---
title: IOU

categories:
  - Object Recognition
  - Object Detection

tags:
  - IOU

mathjax: true
---
# IOU
物体检测需要定位出物体的bounding box, 就像下面的图片一样，我们不仅要定位出车辆的bounding box，我们还要识别出bounding box里面的无力就是车辆.

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/tklIHI.png)

对于bounding box的定位精度，有一个重要的概念：因为我们算法不可能百分百跟人工标注的数据完全匹配，因此就存在一个定位精度评价公式: IOU。  

它定义了两个bounding box的重叠度，如下图所示:  

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/08cc3B.png)

就是矩形A、B的重叠面积占A、B并集的面积比例。

计算公式:

`$ IOU = \frac{A \cap B}{A \cup B}$`