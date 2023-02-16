---
title: Python报RuntimeError NCCL Error 2 unhandled system error

categories:
  - OJ

tags:
  - Programing
---

# Python报RuntimeError NCCL Error 2 unhandled system error
```
docker exec  -it --user root  -e NVIDIA_VISIBLE_DEVICES=0,1,2,3 remote /bin/bash
```
上面的命令，目前好像没用了。。。  

github别人的方法，我通过自己创建了一个新的容器，然后在这基础上进行了配置，发现不会出现RuntimeError: NCCL Error 2: unhandled system error的问题了。
```
docker exec  -it --user root --gpus all --ipc=host  -e NVIDIA_VISIBLE_DEVICES=0,1,2,3 remote /bin/bash
```
需要重新创建一个容器！！！

然后重新配置环境就好了。