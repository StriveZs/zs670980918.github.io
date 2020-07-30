---
title: Non-Maximum Suppression(NMS)

categories:
  - Object Recognition
  - Object Detection
  - 科研

tags:
  - NMS
  - 非极大值抑制

mathjax: true
---

# Non-Maximum Suppression(NMS) 非极大值抑制
## 概述
非极大值抑制(NMS), 顾名思义就是抑制不是极大值的元素，可以理解为局部最大搜索。这个局部代表的就是一个邻域，邻域有两个参数可变，一个是邻域的维数，而是邻域的大小。这里不讨论通用的NMS算法, 而是用于目标检测中提取分数最高的窗口。  

例如在行人检测中，滑动窗口经提取特征，经分类器识别后，每个窗口都会得到一个分数。但是滑动窗口会导致很多窗口和其他窗口存在包含或者大部分交叉的情况。这时就需要用到NMS来选取这些邻域里分数最高(是行人几率最大)，并且一直那些分数低的窗口。  

NMS在计算视觉领域有着非常重要的应用，如视频目标跟踪、数据挖掘、3D重建、目标识别以及纹理分析等。

## NMS在目标检测中的应用
### 人脸检测框重叠例子

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/bWa7my.png)

我们的目标就是要去除冗余的检测框，保留最好的一个。  
有多种方式可以解决这个问题，Triggs建议使用**Mean-shift**算法，利用bbox的坐标和当前图片尺度的对数来检测bbox的多种模式，但是效果可能并没有使用强分类器结合NMS的效果好。  

### 检测目标 pipline
![figure.2](https://gitee.com/zyp521/upload_image/raw/master/RKmAqi.png)

产生proposal后使用分类网络给吃每个框的每类置信度，使用回归网路修正位置，最终应用NMS。

## NMS原理
对于Bounding Box的列表B以及对应的置信度S，采用下面的计算方式，选择具有最大score的检测框M，将其从B集合中移除并加入到最终的检测结果D中，通常将B中剩余检测框中与M的IoU大于阈值Nt的框从B中移除，重复这个过程，直到B为空。

### IoU阈值和排序 
通常阈值设置是0.3-0.5  
其中用到的排序，可以按照右下角的坐标排序或者面积排序，也可以通过SVM等分类器得到的得分或者概率，**R-CNN中就是按照得分进行排序的**.  

### 例子
![figure.3](https://gitee.com/zyp521/upload_image/raw/master/dF8ON9.png)

如上面图片所示，定位一个车辆，最后算法就找出了一堆方框，我们需要判别哪些矩形框是没用的，  
非极大值抑制的方法是: 假设有6个矩形框，根据分类器的类别分类概率做排序，假设从小到大属于车辆的概率，分别为A、B、C、D、E、F。  

- 从最大概率矩形框F开始，分别判断A-E与F的重叠率IoU是否大于某个设定的阈值
- 假设B、D和F的重叠度超过了阈值，那么就扔掉B、D；并表卷积第一个矩形框F，是我们保留下来的。
- 从剩下的矩形框A、C、E中，选择概率最大的E，然后判断E和A、C的重叠度，重叠度大于阈值的就扔掉，将标记E是我们保留下来的第二个矩形框
- 就这样重复上述步骤，直到剩余框集合中没有元素了，那么被保留下来的矩形框就是我们所需要的定位框。

### 代码示例
在R-CNN中使用了NMS来确定最终的bounding-box，其对应每个候选框分别送入分类器，根据分类器的类别分类概率进行排序(greedy-NMS)， 但实际也可以在分类之前运用简单版本的NMS来去除一些框。  

Python实现单类别的NMS:
```
def py_cpu_nms(dets, thresh): 
    """Pure Python NMS baseline.""" 
    #x1、y1、x2、y2、以及score赋值 
    x1 = dets[:, 0] 
    y1 = dets[:, 1] 
    x2 = dets[:, 2] 
    y2 = dets[:, 3] 
    scores = dets[:, 4] 
    
    #每一个检测框的面积 
    areas = (x2 - x1 + 1) * (y2 - y1 + 1) 
    #按照score置信度降序排序 
    order = scores.argsort()[::-1] 
    keep = [] 
    #保留的结果框集合 
    while order.size > 0: 
        i = order[0] 
        keep.append(i) 
        #保留该类剩余box中得分最高的一个 
        #得到相交区域,左上及右下 
        xx1 = np.maximum(x1[i], x1[order[1:]]) yy1 = np.maximum(y1[i], y1[order[1:]]) 
        xx2 = np.minimum(x2[i], x2[order[1:]]) yy2 = np.minimum(y2[i], y2[order[1:]]) #计算相交的面积,不重叠时面积为0 
        w = np.maximum(0.0, xx2 - xx1 + 1) 
        h = np.maximum(0.0, yy2 - yy1 + 1) inter = w * h #计算IoU：重叠面积 /（面积1+面积2-重叠面积） 
        ovr = inter / (areas[i] + areas[order[1:]] - inter) #保留IoU小于阈值的box 
        inds = np.where(ovr <= thresh)[0] 
        order = order[inds + 1] #因为ovr数组的长度比order数组少一个,所以这里要将所有下标后移一位 
    return keep
```

Faster R-CNN的MATLAB和python版本实现一致，对于对类别的NMS，就是加了一层for循环来对每个类别进行NMS而已。

### NMS Loss
值得注意的是对多类别检测任务，如果对每类进行NMS，那么当检测结果中包含两个被分到不同的目标且其IoU较大时，会得到不可接受的结果，如下图所示:

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/Fd380c.png)

一种改进方式便是在损失函数中加入一部分NMS损失。NMS损失可以定义为与分类损失相同：`$ L_{nms}=L_{cls}(p,u)=-log_{p_{u}} $`, 即真实类别u对应log损失，p是C个类别的预测概率，实际相当于增加分类误差。

### Sotf-NMS
上述NMS算法的一个主要问题是当两个ground-truth的目标的重叠度很高时，NMS会将具有较低置信度的去掉, 如下图所示：

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/1SliMR.png)

如上图所示，红框和绿框的重叠度很大，应该超过了一般大家所设定的阈值，因此在NMS算法中由于绿框的置信度为0.8而红框为0.95，因此NMS算法会将绿框去掉，这样是不正确的。  

在Soft-NMS中对NMS这个缺陷进行改进：

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/kSvvcn.png)

改进方法在于将置信度改为IoU的函数: f(IoU)，具有较低的值而不至于从排序列表中删去。

两种形式的IoU函数:
- 线性函数：即将需要取出的框的置信度改为1-重叠值, 函数值不连续，在某一点的值发生跳跃

`$ s_{i}=\left\{\begin{matrix} s_{i}\:\:\:\:iou(M,b_{i})<N_{t} \\ s_{i}(1-iou(M,b_{i}))\:\:\:\: iou(M,b_{i}) \geq N_{t} \end{matrix}\right. $`

- 高斯函数，时间复杂度同传统的greedy-NMS, 为`$ \sigma (N^{2}) $`

`$ s_{i}=s_{i}e \frac{-iou(M,b_{i}^{2})}{\sigma},\forall b_{i} \notin D $`

#### 代码
```
ua = float((tx2 - tx1 + 1) * (ty2 - ty1 + 1) + area - iw * ih) ov = iw * ih / ua #iou between max box and detection box 
if method == 1: # linear 
    if ov > Nt: 
        weight = 1 - ov 
    else: 
        weight = 1 
elif method == 2: # gaussian 
    weight = np.exp(-(ov * ov)/sigma) 
else: # original NMS 
    if ov > Nt: 
        weight = 0 
    else: 
        weight = 1 
        
# re-scoring 修改置信度 
boxes[pos, 4] = weight*boxes[pos, 4]
```

基于proposal方法的模型结果上应用比较好，检测效果提升:

![figure.7](https://gitee.com/zyp521/upload_image/raw/master/6qkPNP.png)

在R-FCN以及Faster R-CNN模型中的测试阶段运用Soft-NMS，在MS-COCO数据集上能够获得大约1%的提升。如果应用到训练阶段的proposal选取过程理论上也能获得提升，在自己的实验中发现确实对易重叠的目标类型有提高(目标不一定真在像素上重叠，切斜的目标的矩形边框会有较大的重叠)，而在SSD、YOLO等非proposal方法中没有提升。