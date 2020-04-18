## 0. 目录
#### 1. [概述与安装](http://10.158.134.250/shiyf/laspview---guid-and-download/edit/master/README.md)
#### 2. [本地端LaspView.exe使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/LaspView.exe.md)
#### 3. [中转端TransitServer.py+远程端Easy.py使用指南](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/Tansit&remote.md)
#### 4. [遭遇防火墙问题](http://10.158.134.250/shiyf/laspview---guid-and-download/blob/master/%23firewall.md)


# 二、 本地端LaspView使用指南

## 控制
> 基本与MS一致  

|  一般模式         | 效果          |  编辑模式            | 效果          |
|  :----:           | :----:        |  :----:              | :----:        |
|  鼠标右键         | 旋转镜头      | LCtrl+鼠标右键       |  旋转选中原子 |
| 鼠标中键/LShift   | 平移镜头      | LCtrl+鼠标中键/LShift|  平移选中原子 |
| 鼠标滚轮          |  镜头缩放     | Delete / BackSpace   |  删除选中原子 |
| ----              |----           | ----                 |----           |
|  鼠标左键 单击    | 选中单个原子  | LCtrl+C              |   复制选中原子|
|  鼠标左键 拖曳    | 框选多个原子  | LCtrl+V              |   粘贴选中原子|
| LCtrl+鼠标左键   | 追加选中      | 



> 鼠标左键单击为选中球体/碰撞器，框选为选中框内球心，拾取方式略有不同  
> 待添加功能包括：超胞、Ctrl+Z等、改元素等
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_3.PNG" width="40%">   

## 菜单栏
### 左侧
菜单栏的每个按钮对应一个面板，内容如下： 、

1. Project:
    - 多个文件间的切换  
2. File：  
    - 打开文件  
    - 保存当前结构  
    - Windows支持将arc文件拖入窗口以打开文件
3. Display：
    - （施工中）  
4. Edit：  
    - 按下后将进入编辑模式，允许修改原子位置
    - 期间锁定其他功能按钮。再次按下后退出，并保存
    - 添加原子
    - 修改晶胞参数等  
  
 
### 右侧

1.  LASP：
    - 进行LASP的本地运算
    - 创建任务后，通过UI或内置文本编辑器修改lasp.in
    - 自动生成运算目录并启动LASP
    - 目前仅支持SSW和NN，CMD黑框消失即运算完成
2.  Server：
    - 与中转服务器进行文件传输
    - 具体使用参见后文


## 工具栏/状态栏
位于最下方，单一arc文件中多帧的切换，和一些信息提示
1. 工具栏：
    - 依次为：第一帧、前一帧、聚焦中心、后一帧、最后一帧
2. 状态栏左侧消息：
    - 第几帧、能量
3. 状态栏右侧消息：
    - 报错消息、其他消息等
