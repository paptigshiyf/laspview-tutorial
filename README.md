# LaspView 下载与使用说明  
LaspView是LASP程序包配套的分子结构可视化工具，主要使用Unity程序及部分python编写，主要特性包括：  
* 轻量化的3D分子结构演示、编辑
* 同一*.arc文件中多个结构的切换
* 通过远程服务器的命令行，发送文件到本地并演示  
* 发送文件到远程服务器，再使用命令行拉取到当前目录

目前仅支持LASP使用的*.arc格式或Material Studio使用的*.car格式
>使用这种标签的内容可跳过  
>项目源码参见 [此处](http://10.158.134.250/shiyf/laspview)，加入项目后才能看见源码，请喊我

# 下载
__本地端下载: ```/home9/shiyf/LaspViewDownload/```内有最新版本__


# 0. 目录
#### 1. [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 2. [本地端LaspView.exe使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 3. [中转端TransitServer.py+远程端Easy.py使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 4. [遭遇防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/%23firewall.md)

  
  

# 1. 概述与安装
LaspView目前分为三个部分：
* 本地端/Laspview.exe
* 中转端/TransitServer.py
* 远程端/TransitServer.py  

## a.本地端Laspview.exe
**本地端提供了3D分子结构的本地渲染演示、动画及编辑**  
仅本地端需要下载在个人电脑上，双击```LaspView.exe```即可运行程序，应可以看到默认打开的文件
请尝试鼠标右键拖动旋转、中键拖动平移等操作是否顺畅


## b.中转端TransitServer.py
出于各种原因，目前的架构是在node1上设置了中转服务器，进行文件的转发  
整体上是两个包含简单协程的服务端，使用asyncio编写，支持并发  
目录在```node1:/home/LaspViewTransit/```下  
> 应该还算稳定，一般不用管，~~死了喊我~~  


## c.远程端Easy.py
使用命令行参数控制发送文件、接收文件、管理中转临时目录```node1:/home/LaspViewTransit/Temp/$USER```等  
目录在```/home9/shiyf/bin/Easy.py```，建议cp至自己的.bashrc中的目录中
```
cp /home9/shiyf/bin/Easy.py /home2/$USER/bin
```