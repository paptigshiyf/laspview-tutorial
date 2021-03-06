# 目录
#### 一、 [概述与安装](https://github.com/paptigshiyf/laspview-tutorial/blob/master/README.md)
#### 二、 [本地端LaspView](https://github.com/paptigshiyf/laspview-tutorial/blob/master/LaspView.exe.md)
#### 三、 [网络通信部分](https://github.com/paptigshiyf/laspview-tutorial/blob/master/Tansit&remote.md)
#### 四、 [防火墙问题](https://github.com/paptigshiyf/laspview-tutorial/blob/master/firewall.md)
<br></br>
# 二、 本地端LaspView

## 1. 控制
> 基本与MS一致  

|  操作       | 效果          |     操作        | 效果          |
|  :----:           | :----:        |  :----:              | :----:        |
|  鼠标右键         | 旋转镜头      | LCtrl+鼠标右键       |  旋转选中原子 |
| 鼠标中键/LShift   | 平移镜头      | LCtrl+鼠标中键/LShift|  平移选中原子 |
| 鼠标滚轮          |  镜头缩放     | Delete / BackSpace   |  删除选中原子 |
| ----              |----           | ----                 |----           |
|  鼠标左键 单击    | 选中单个原子  | LCtrl+C              |   复制选中原子|
|  鼠标左键 拖曳    | 框选多个原子  | LCtrl+V              |   粘贴选中原子|
| LCtrl+鼠标左键   | 追加选中      |  LCtrl+Z / Escape     | 撤回编辑操作  |



> 鼠标左键单击为选中球体/碰撞器，框选为选中框内球心，拾取方式略有不同  
> 待添加功能包括：改元素等
<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_3.PNG" width="70%">   

## 2. 菜单栏
### 左侧
菜单栏的每个按钮对应一个面板，按下即显示，再按即隐藏，内容如下： 、

1. Project:
    - 多个文件间的切换  
2. File:
    - 打开文件  
    - 保存当前结构  
    - Windows支持将arc文件拖入窗口以打开文件
3. Display:
    - 修改背景颜色
    - 播放动画的时间间隔
    - 显示多个周期/Lattice
    - 修改球棍模型的具体参数
4. Edit:
    - 现在无需按下Edit按钮即可修改结构
    - 添加原子、修改晶胞参数、超胞
    - 弹出的小窗口可用鼠标左键或中键拖动

  
 
### 右侧
1.  Server：
    - 按下```Server```+```Start Listening```准备接受arc文件
    - 按下```Send Structure```发送当前结构到<kbd>node1</kbd> ```Temp```目录
    - 作业目录下使用```Easy.py -cl```将文件复制到当前目录
    - 具体使用参见后文 请避免发送all.arc等大文件


## 3. 工具栏/状态栏
位于最下方，单一arc文件中多帧的切换，和一些信息提示
1. 工具栏：
    - 依次为：第一帧、前一帧、聚焦中心、播放演示、后一帧、最后一帧
    - 播放演示默认为0.2s一帧，时间间隔再Display面板中设置
2. 状态栏左侧消息：
    - 第几帧、能量，可手动输入帧数
3. 状态栏右侧消息：
    - 报错消息、其他消息等
