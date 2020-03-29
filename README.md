# LaspView 下载与使用说明  
LaspView是LASP程序包配套的分子结构可视化工具，主要使用Unity程序及部分python编写，主要特性包括：  
* 轻量化的3D分子结构演示、编辑  
* 同一*.arc文件中多个结构的切换
* 通过远程服务器的命令行发送文件到本地演示或接收文件  

目前仅支持LASP使用的*.arc格式或Material Studio使用的*.car格式
>使用这种标签的内容可跳过
## 1. 概述与安装
LaspView目前分为三个部分：
* 本地端/Laspview.exe
* 中转端/TransitServer.py
* 远程端/TransitServer.py  

### 本地端Laspview.exe
**本地端提供了3D分子结构的渲染本**  
仅本地端需要安装在个人主机上，点击链接下载最新版本  
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


### 中转端TransitServer.py
目前的架构是在node1上设置了中转服务器，进行文件的转发  
目录在```node1:/home/LaspViewTransit/```下
> **远程端发送文件到本地端的流程:**
>  
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_1.PNG" width="60%">  
>   
> **本地端发送文件到远程端的流程:**  
>   
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_2.PNG" width="60%">  

## 2. 本地端/Laspview.exe 
## 3. 中转端/TransitServer.py
## 4. 中转端/TransitServer.py