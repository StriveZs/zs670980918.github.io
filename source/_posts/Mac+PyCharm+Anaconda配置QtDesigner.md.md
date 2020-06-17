# Mac+PyCharm+Anaconda配置QtDesigner
打开Pycharm->Perference->Tools->ExternalTools 添加下面两个外部工具。

## 配置QtDesigner
首先说明一下由于我这里是使用Anaconda进行配置的，因此我的路径可能和你默认使用的路径不同，下面我给出两种路径:
```
Anaconda:
~opt/anaconda3/bin/Designer.app

Mac默认路径：
/usr/localCellar/qt/5.10.1/libexec
```

下面是QtDesigner的配置信息，按照下图配置即可：

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/H2IeEC.png)

## 配置PyUIC
下面添加将.ui文件转换为.py文件的外部工具。

具体配置如下图：

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/GQ8xLh.png)

- Program：选择python就可以了地址为：~/opt/anaconda3/bin/python3.7
- Arguments：-m PyQt5.uic.pyuic $FileName$ -o $FileNameWithoutExtension$.py
- Working directory：$ProjectFileDir$

## 启动
直接在Tools->Externel Tools中选择QtDesigner。  

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/d0dsHg.png)

保存的文件一定要放在工作目录下，然后在选择PyUIC外部工具将ui选择为py文件。