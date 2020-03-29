# 2. 本地端LaspView.exe使用指南

## 控制
> 基本类似MS  

|  操作             | 效果          |
|  :----:           | :----:        |
|  鼠标右键         | 旋转镜头      |
| 鼠标中键          | 平移镜头      |
| 鼠标滚轮          |  镜头缩放     |
| ----              |----           |
|  鼠标左键         | 选中原子      |
| 左Ctrl+鼠标左键   | 追加选中      |
| ----              |----           |
| 左Ctrl+鼠标中键   |  平移选中原子 |
| 左Ctrl+鼠标右键   |  旋转选中原子 |
| Delete            |  删除选中原子 |

_鼠标左键短摁进行单选，长摁进行框选，拾取方式略有不同_  

<img src="http://10.158.134.250/shiyf/laspview---guid-and-download//raw/master/Assets/laspview_3.PNG" width="50%">   

## 工具栏/状态栏
按钮依次为：第一帧、前一帧、聚焦在晶格中心点、后一帧、最后一帧

## 菜单栏
### 左侧
Project面板：   多个文件间的切换  
File面板：      打开、保存文件；共用按钮上方的输入栏作为路径  
Display、Edit施工中  
### 右侧


Server面板：  

|  按钮         |   效果      |
|  :----:       | :----:    |
|  LocalIP      | 本地IP，启动时自动读取一次    |
| ServerIP      |   node1 IP   |
|CheckLocalIP   |  IP更改后需要更新本地IP，常见于VPN断了重连|
|SendLocalIP    |  将本地IP发送给中转端|
|SendStructure  |  将当前帧的结构发送给中转端|

文件传输的具体使用将在Easy.py中介绍