# 目录
#### 一、 [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 二、 [本地端LaspView](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 三、 [网络通信部分](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 四、 [防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/firewall.md)
<br></br>
# 三、网络通信部分 
## 1. 使用指南
### 1) 配置用户
如需使用网络通信部分，请修改```LaspViewConsole.log```，在压缩文件中已经设置了该文件的链接，双击即可
修改其中的```user```，使其与服务器上的用户名相同，如
```
user=$USER
```
将```Easy.py```加入自己的$PATH目录，一般应已加入。如未找到该文件，请```cp```到自己的目录
```
cp /home9/shiyf/bin/Easy.py /home2/$USER/bin
```
> 现已无需手动修改Easy.py中的user，仅需修改LaspViewConsole.log中的user

### 2) 远程发送文件到本地
* <b>LaspView.exe: 点击<kbd>Server</kbd>打开Server面板

* <b>LaspView.exe: <kbd>Server</kbd>面板 点击<kbd>Start Listening</kbd></b> 
    - 开启本地端的监听
    - 如未断网，操作一次即可
    - 第一次使用时，Windows可能询问是否允许使用网络服务，请选是
* <b>Shell：```[shiyf@storage4 dir]$``` ```Easy.py best.arc``` 或 ```Easy.py -s best.arc```</b>
    - 发送文件到本地，可无限次发送。
    - 如无网络问题或防火墙问题，LaspView应该已经显示```best.arc```的最后一帧了
    - 请保证文件名尾缀```*.arc```，否则不会读取  
    - 请避免发送过大的文件到本地，目前已经做了一定限制，最大接收约1M的文件，避免罚站/无响应

> * 若等待时间>5s
>   - 请中止Easy.py并检查网络状况,比如是否曾发送本地IP，是否已经开启监听  
>   - 其他意外情况请参见 防火墙设置
>
> 目前使用的python3.6，我没有找到设置连接超时上限的参数，默认的链接超时为1min，可能1min后才会报```Connect call failed```

### 3) 本地发送结构到远程
* <b>LaspView.exe: <kbd>Server</kbd>面板 点击<kbd>Send Structure</kbd></b> 
    - 发送当前帧的结构
    - 中转端接收文件写在临时目录<kbd>node1</kbd>```/home/LaspViewTransit/template/$USER/```下  
    - 文件名称是自动生成的，为```{随机数}-{时间}.arc```
* <b>Shell：```[shiyf@storage4 dir]$``` ```Easy.py -cl``` 或 ```Easy.py --copylatest```</b>
    - 将临时目录中，更新时间最新的文件，拉取到当前<kbd>工作目录</kbd>
    - 可以再```Easy.py *.arc```发回去看看对不对

以上即基本的文件传输操作。
<br></br><br></br>
## 2. 详细内容
这一部分将详细介绍一些参数和其他选项，类似于手册。   
其中，<b>只有第三部分 3) 远程端  介绍Easy.py的部分可能相对实用</b>，看那个就好  
实际上```Easy.py -h```亦有一部分帮助内容
### 1) 本地端
Server面板的内容如下  

|  按钮         |   说明      |
|  :----:       | :----:    |
|   Server Btn  | 菜单栏的Server按钮，点击时将自动从DNS和ipconfig读取本机ip，并Send Local IP| 
|  Local IP      |  本地IP，启动时自动读取一次 |
| Server IP      |   node1 IP    |
|Stop Listening |  开启监听后出现，关闭监听|
|Start Listening |  开启监听，允许接收结构 |
|Send Local IP    |  将本机的IP发送给中转端，让中转端记录 |
|Send Structure  |  将当前帧的结构发送到远程 |


### 2) 中转端
中转端的启动、停止基本不用管， ~~出问题喊我~~

###### 启动
登录node1并```cd /home/LaspViewTransit/```，```nohup```启动已经写在job.sh内，执行以下命令即可:
```
[shiyf@node1 LaspViewTransit]$ ./job.sh
```
###### 硬杀
需要启动进程的用户或root来杀, 首先获得进程PID:
```Bash
[shiyf@node1 LaspViewTransit]$ netstat -lp | grep python
 ```
 或：
```Bash
[shiyf@node1 LaspViewTransit]$ ps | grep python
 ```
得到PID如```1553```，再杀掉
```Bash
[shiyf@node1 LaspViewTransit]$ kill -9 1553
```

###### 软杀
无需登录node1， 使用Easy.py：
```Bash
[shiyf@storage4 dir]$ Easy.py -kill
```
即会发送信号令TransitServer.py自杀

## 3. 远程端Easy.py
除了--user以外，Easy.py每次运行都只能使用一个参数，当使用多个参数时只认一个  

|  命令行参数  |   例子      | 效果|
|  :----:      | ----   |----   |
| -s / --send  | ```Easy.py -s 1.arc [2.arc]``` | 将文件发送到本地，支持多个文件同时发送|
|              | ```Easy.py 1.arc```| 没有使用可选参数时，默认为发送文件|
| -ls / --list | ```Easy.py -ls```| 列出用户的临时目录下的文件 |
| -cl / --copylatest | ```Easy.py -cl```| 拉取临时目录下最新的一个文件到本地 |
|               | ```Easy.py -cl  3```| 拉取临时目录下最新的3个文件到本地 |
| -cp / --copy | ```Easy.py -cp 91990-0328073607.arc``` | 拉取临时目录下的特定文件到本地，支持同时拉取多个文件|
|              | ```Easy.py -cp 9```  | 可以使用python风格的正则表达式(实际是re.match的patten)，拉取文件到当前目录|
| -clear       | ```Easy.py -clear``` | 清理删除用户的临时目录下的所有文件 |
| -kill        | ```Easy.py -kill```  | 令中转端TransitServer自杀|
| -u / --user  | ```Easy.py -user zpliu -s 1.arc``` | 变更用户名，向其他用户的本地端发送1.arc |


> **远程端发送文件到本地端的流程:**
>  
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_1.PNG" width="40%">  
>   
> **本地端发送文件到远程端的流程:**  
>   
> <img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_2.PNG" width="40%">  

