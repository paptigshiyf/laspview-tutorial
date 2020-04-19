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


# 目录
#### 一、 [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 二、 [本地端LaspView](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 三、 [网络通信部分](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 四、 [防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/firewall.md)

<br></br>
  

# 一、概述与安装
LaspView目前分为三个部分：
* 本地端/Laspview.exe
* 中转端/TransitServer.py
* 远程端/TransitServer.py  

## 1.本地端Laspview.exe
本地端使用Unity3D编写，提供了分子结构的**本地渲染演示、动画及编辑**  
仅本地端需要下载在个人电脑上，双击```LaspView.exe```即可运行程序，应可以看到默认打开的文件  
请尝试鼠标右键拖动旋转、中键拖动平移等操作是否顺畅

## 2.中转端TransitServer.py
出于种种考虑，在<kbd>node1</kbd>上架了一个中转服务器进行**文件转发**。
整体上是两个包含简单协程的服务端，使用asyncio编写，支持并发  
目录在<kbd>node1</kbd>```/home/LaspViewTransit/```下  
> 应该还算稳定，一般不用管，~~死了喊我~~  

## 3.远程端Easy.py
在使用EasyConnect等校园局域网VPN后，在Shell中，使用使用命令行参数控制**发送文件、接收文件**
目录在```/home9/shiyf/bin/Easy.py```，建议```cp```或者```ln -s```至自己的的目录中
```
cp /home9/shiyf/bin/Easy.py /home2/$USER/bin
```
<b>正确配置</b>且防火墙无碍后，在LaspView界面中开启监听，并在Shell的<kbd>工作目录</kbd> 使用如下命令，即可在LaspView中演示结构：
```
Easy.py best.arc
```
在LaspView界面中发送结构，并在Shell的<kbd>工作目录</kbd> 使用如下命令，即可将结构发送至<kbd>工作目录</kbd>：
```
Easy.py -cl
```


> 文件流的传输如下：  
> * <kbd>工作目录</kbd>发送至<kbd>本地</kbd>:
>    * <kbd>工作目录</kbd>```Easy.py best.arc``` -> <kbd>node1</kbd>的内存 -> <kbd>本地</kbd> ```Temp``` 目录 -> LaspView读取  
> * <kbd>本地</kbd>发送至<kbd>工作目录</kbd>:
>     * <kbd>本地</kbd>-><kbd>node1</kbd> ```Temp```目录-> <kbd>工作目录</kbd>```Easy.py -cl``` -> <kbd>工作目录</kbd>  