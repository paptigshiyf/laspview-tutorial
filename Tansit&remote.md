# 中转端TransitServer.py+远程端Easy.py使用指南
## 中转端TransitServer
> 整体上不用管 ~~（但愿，出问题喊我）~~

> ### 启动
> 登录node1并```cd /home/LaspViewTransit/```，使用```nohup```启动，已经写在job.sh内，执行以下命令即可:
> ```Bash
> [shiyf@node1 LaspViewTransit]$ ./job.sh
> ```
> ### 关闭
> ##### 硬杀
> 需要启动进程的用户或root来杀
> 首先:
> ```
> [shiyf@node1 LaspViewTransit]$ netstat -lp | grep python
> ```
> 或：
> ```
> [shiyf@node1 LaspViewTransit]$ ps | grep python
> ```
> 得到PID， 比如```1553```，再
> ```
> [shiyf@node1 LaspViewTransit]$ kill -9 1553
> ```
> 即可杀掉
> ##### 软杀
> 无需登录node1， 使用Easy.py, 假使Easy.py已在$PATH中
> ```
> [shiyf@storage4 LaspViewTransit]$ Easy.py -kill
> ```
> 即会发送信号令TransitServer.py自杀