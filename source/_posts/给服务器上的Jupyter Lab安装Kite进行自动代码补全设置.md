---
title: 给服务器上的Jupyter Lab安装Kite进行自动代码补全设置

categories:
  - Linux
  - Jupyter
  - 服务器

tags:
  - Linux
  - Jupyter
  - 服务器
  - Python
  - Kite
---

# 给服务器上的Jupyter Lab安装Kite进行自动代码补全设置
## 安装Jupyter Lab
使用如下命令安装Jupyter Lab:
```
conda install juputerlab
```
## 安装Kite
这里我是在docker中安装的kite，需要下载kite的安装包，又因为docker容器内没有wget，因此现需要安装wget，使用如下命令:
```
sudo apt-get install wget
```
安装完成wget之后使用如下命令安装kite：
```
bash -c "$(wget -q -O - https://linux.kite.com/dls/linux/current)"
```
想要关闭的时候直接在 htop 面板中找到 pid 然后将进程 kill 掉即可。

## 设置Kite开机自启
根据给的提示可以看出需要使用命令进行如下操作:
```
[installer] kite is installed! launching now! happy coding! :)
[installer] with systemd, run systemctl --user start kite-autostart
[installer] without systemd, run /home/user/.local/share/kite/kited
[installer] 	or launch it using the Applications Menu
Removing kite-installer
```

由于我是在docker中运行的，没有systemd命令，因此需要先使用如下命令安装systemd:
```
sudo apt-get install --reinstall systemd
sudo apt-get install systemd
```

安装完成之后，使用如下命令设置kite自动运行:
```
sudo systemctl --user start kite-autostart
```
### 手动开启 每次启动docker都要打开
如果没有安装systemctl成功的话，可以使用手动的方式进行启动, 命令如下:
```
/home/user/.local/share/kite/kited
```

## 为Jupyter Lab安装Kite扩展
对于 3.0 版本以上的 JupyterLab，运行如下命令:
```
pip install "jupyterlab-kite>=2.0.2"
```
亲测conda install安装失败了不知道为啥。  

完成以上两步以后重启 JupyterLab，会自动弹出一个 Kite 的教程。

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/OSNQAf.png)

等待kite ready即可

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/JNV0ls.png)