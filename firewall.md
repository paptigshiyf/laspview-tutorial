# 目录
#### 一、 [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 二、 [本地端LaspView](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 三、 [网络通信部分](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 四、 [防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/firewall.md)
<br></br>
# 四、如果遭遇防火墙问题
#### 1. 正常情况
> 一般本地接收结构可能遭遇防火墙问题，本地发送结构应该问题不大  
> 欢迎直接呼叫shiyf售后

在本地端LaspView第一次使用Start Listening打开监听的时候，若跳出“是否允许LaspView使用网络”之类的窗口，并允许之，应不会有防火墙问题  
如果仍然无法正常接收```Easy.py -s best.arc```发来的结构，请首先检查网络状况：
* 是否连接了校园网VPN
* 是否已经向中转端<kbd>node1</kbd>发送过本地IP地址（按钮<b>Send Local IP</b>）
* 尝试变更下拉框<b>Local IP</b>中的IP地址

> 此外，文件必须得是*.arc的文件后缀，否则不认

如果仍不能发送到本地，请尝试关闭防火墙：
* Win10：搜索防火墙 > 防火墙和网络保护 > 关掉防火墙

如果关了防火墙仍无法联通，请呼叫shiyf售后   
如果关了防火墙能够联通，请手动配置防火墙入站规则

#### 2. 手动配置防火墙入站规则

* 防火墙和网络保护 > 高级设置 > 入站规则  
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/firewall_1.png" width="40%">   <br></br>
* 新建规则  
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/firewall_2.png" width="40%">   <br></br>
* 类型：端口  >     TCP，允许9540端口  
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/firewall_3.png" width="40%">   <br></br>
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/firewall_4.png" width="40%">   <br></br>
* 设置名称（任意，如LaspView）> 完成  
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/firewall_5.png" width="40%">   <br></br>

如果仍不能解决，请呼叫shiyf售后