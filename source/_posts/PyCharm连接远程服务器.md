---
title: PyCharm连接远程服务器

categories:
  - Python

tags:
  - Python
  - PyCharm
  - Linux
  - 服务器
---

# PyCharm连接远程服务器
使用PyCharm连接远程服务器，并使用服务器的解释器和代码文件来进行运行。

## 配置Deplotment
在这之前首先建议，要单独创建一个项目文件夹，因为当前项目的文件都会被自动上传上去。

![figure.1](https://pic1.zhimg.com/80/v2-b499139f685fe9d8615d4287c0bff230_1440w.jpg)

![figure.2](https://pic3.zhimg.com/80/v2-c2be0d6a5587784bcac2658aac39d106_1440w.jpg)

选择你的服务器的地址和你本地的地址:  

![figure.3](https://pic4.zhimg.com/80/v2-ad6ee2f63c3d36236a5c796f7810aa2f_1440w.jpg)

## 配置解释器
该项目现在使用的就是远程服务器上的Python解释器了。以后的项目若想/不想使用该解释器，手动更改解释器即可。  
目前来说直接配置解释器就可以完成上面的Deployment的操作.

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/D2JQ9A.png)

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/G8MUAj.png)

![figure.6](https://gitee.com/zyp521/upload_image/raw/master/V9UfmX.png)

## 测试
新建一个文件，然后同步上去直接使用如下代码进行测试:
```
print('hello')
import torch
flag = torch.cuda.is_available()
print(flag)
ngpu= 1
# Decide which device we want to run on
device = torch.device("cuda:0" if (torch.cuda.is_available() and ngpu > 0) else "cpu")
print(device)
print(torch.cuda.get_device_name(0))
print(torch.rand(3,3).cuda())
```

出现如下结果:
```
hello
True
cuda:0
GeForce RTX 2080
tensor([[0.3170, 0.4412, 0.3377],
        [0.5438, 0.0894, 0.6420],
        [0.0981, 0.2753, 0.0179]], device='cuda:0')
```

则表明成功了。