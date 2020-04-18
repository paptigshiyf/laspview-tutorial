# LaspView 下载与使用说明  
LaspView是LASP程序包配套的分子结构可视化工具，主要使用Unity程序及部分python编写，主要特性包括：  
* 轻量化的3D分子结构演示、编辑  
* 同一*.arc文件中多个结构的切换
* 通过远程服务器的命令行，发送文件到本地并演示  

目前仅支持LASP使用的*.arc格式或Material Studio使用的*.car格式
>使用这种标签的内容可跳过  
>项目源码参见 [此处](http://10.158.134.250/shiyf/laspview)，加入项目后才能看见源码，请喊我

# 下载
__本地端下载: ```/home9/shiyf/LaspViewDownload/```内有最新版本__


## 0. 目录
#### 1. [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 2. [本地端LaspView.exe使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 3. [中转端TransitServer.py+远程端Easy.py使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 4. [遭遇防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/%23firewall.md)

## 1. 概述与安装
LaspView目前分为三个部分：
* 本地端/Laspview.exe
* 中转端/TransitServer.py
* 远程端/TransitServer.py  

### 0. 安装太长不看版:
* ```/home9/shiyf/LaspViewDownload/``中下载最新版本LaspView
* 改```laspview allkey.log```里的```user```
* ```cp /home9/shiyf/bin/Easy.py 自己的PATH目录```

### a.本地端Laspview.exe
**本地端提供了3D分子结构的渲染演示及编辑**  
仅本地端需要安装在个人电脑上，  
解压程序包后，请打开```allkey.log```文件:
```
remote_ip=10.158.134.241
remote_port=9538
local_port=9540
laspin_default=lasp.in
arc_default=10-12-10best.arc
user=shiyf
```
修改用户名```user```, 如```user=shiyf-desktop```  
其余设置无需更改。双击```LaspView.exe```即可运行程序，应可以看到默认打开的文件
> 目前，该用户名无需与我组服务器上的用户名一致，但后可能会建立白名单机制，建议与服务器一致  


### b.中转端TransitServer.py
目前的架构是在node1上设置了中转器，进行文件的转发  
整体上是一个包含简单协程的Server，使用asyncio编写，支持并发  
目录在```node1:/home/LaspViewTransit/```下  
> 基本不用管：感觉还算稳定，~~死了喊我~~  

> **远程端发送文件到本地端的流程:**
>  
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_1.PNG" width="60%">  
>   
> **本地端发送文件到远程端的流程:**  
>   
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_2.PNG" width="60%">  

### c.远程端Easy.py
使用命令行参数控制发送文件、接收文件、管理中转临时目录```node1:/home/LaspViewTransit/template/$USER```等  
目录在```/home9/shiyf/bin/Easy.py```，建议cp至自己的.bashrc中的目录中，如
```
cp /home9/shiyf/bin/Easy.py /home2/$USER/bin
```
并修改用户名```USER```，应与本地端的```allkey.log```一致，如```user="shiyf-desktop"```  
```
"""CHANGEABLE PARAMETERS for USER"""
USER = "shiyf"
TEMP = './template'
```