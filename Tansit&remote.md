## 0. 目录
#### 1. [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 2. [本地端LaspView.exe使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 3. [中转端TransitServer.py+远程端Easy.py使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 4. [遭遇防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/%23firewall.md)


|  按钮         |   效果      |
|  :----:       | :----:    |
|  LocalIP      | 本地IP，启动时自动读取一次    |
| ServerIP      |   node1 IP   |
|CheckLocalIP   |  IP更改后需要更新本地IP，常见于VPN断了重连|
|SendLocalIP    |  将本地IP发送给中转端|
|SendStructure  |  将当前帧的结构发送给中转端|

# 三. 网络通信部分  

## 1. 本地端
如需使用网络通信部分，请先在本地端```LaspView.exe```所在目录中修改```LaspViewConsole.log```中的```user```
```
user=shiyf
```

## 2. 中转端
出于种种考虑，在<kbd>node1</kbd>上架了一个中转服务器进行文件转发。文件流的传输如：  
* <kbd>工作目录</kbd>发送至<kbd>本地</kbd>:
    * <kbd>工作目录</kbd>```Easy.py best.arc``` -> <kbd>node1</kbd>的内存 -> <kbd>本地</kbd> ```Temp``` 目录 -> LaspView读取  
* <kbd>本地</kbd>发送至<kbd>工作目录</kbd>:
    * <kbd>本地</kbd>-><kbd>node1</kbd> ```Temp```目录-> <kbd>工作目录</kbd>```Easy.py -cl``` -> <kbd>工作目录</kbd>  
<br></br>

中转端的启动、停止基本不用管，可跳过 ~~出问题喊我~~

> ### 启动
> 登录node1并```cd /home/LaspViewTransit/```，```nohup```启动已经写在job.sh内，执行以下命令即可:
> ```Bash
> [shiyf@node1 LaspViewTransit]$ ./job.sh
> ```
> ### 关闭
> ##### 硬杀
> 需要启动进程的用户或root来杀
> 首先:
> ```Bash
> [shiyf@node1 LaspViewTransit]$ netstat -lp | grep python
> ```
> 或：
> ```Bash
> [shiyf@node1 LaspViewTransit]$ ps | grep python
> ```
> 得到PID， 比如```1553```，再
> ```Bash
> [shiyf@node1 LaspViewTransit]$ kill -9 1553
> ```
> 即可杀掉
> ##### 软杀
> 无需登录node1， 使用Easy.py, 假使Easy.py已在$PATH中
> ```Bash
> [shiyf@storage4 dir]$ Easy.py -kill
> ```
> 即会发送信号令TransitServer.py自杀

## 远程端Easy.py
包含了一个和中转端通信的client，发送并接收信息。默认Easy.py已在$PATH中
### Shell命令行发送文件到本地
首先应使本地端发送本地IP到中转端，并开启本地端的监听:
```
LaspView.exe: Server面板中依次点击（CheckLocalIP）> SendLocalIP > StartListening
```
开启监听后，Windows可能询问是否允许使用网络服务，请选是

其次在shell中执行```Easy.py```,使用```-s```/```--send```参数发送文件。
```
[shiyf@storage4 dir]$ Easy.py -s best.arc
```
此时本地端应该可以显示该文件。  
请保证文件名尾缀```*.arc```，否则收到也不会读取  
请避免发送过大的文件到本地，目前已经做了一定限制，最大接收约1M的文件

> #### 若等待时间>5s
> 请中止Easy.py并检查网络状况,比如是否曾发送本地IP，是否已经开启监听  
> 其他意外情况请参见 防火墙设置
>
> 目前的python3.6，我没有找到设置连接超时上限的参数，默认的链接超时为1min，也就是说1min后才会报```Connect call failed```

### 本地发送结构到远程
可能是最常用的东西，建议记一下各个命令行参数
本地端将当前结构(目前正在演示的结构，单一结构)发送至中转端:
```
LaspView.exe: Server面板中点击SendStructure
```
中转端会将文件记录在临时目录```node1:/home/LaspViewTransit/template/$USER/```下  
文件名称是自动生成的，为```{随机数}-{时间}.arc```  
可使用```Easy.py```的```-ls```/```--list```参数检查临时目录下的文件:
```Bash
[shiyf@storage4 dir]$ Easy.py -ls
91990-0328073607.arc   23087-0328071510.arc   36959-0328071510.arc
```
可使用```Easy.py```的```-cp```/```--copy```参数拷贝文件至当前目录  
```Bash
[shiyf@storage4 dir]$ Easy.py -cp 91990-0328073607.arc
cp succeed: 91990-0328073607.arc
```
可使用```Easy.py```的```-clear```/```--clear```清理临时目录```/template/$USER/```
```Bash
[shiyf@storage4 dir]$ Easy.py -clear
All file in template is cleared
```


> **远程端发送文件到本地端的流程:**
>  
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_1.PNG" width="60%">  
>   
> **本地端发送文件到远程端的流程:**  
>   
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_2.PNG" width="60%">  

以上
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/ququ.jpeg" width="20%">  
