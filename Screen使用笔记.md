## Screen工具从入门到献舍

> Screen可以让用户在Linux中创建一个远程会话并且在断开连接后会话中正在执行的程序将得到保留

1. screen常用命令

   ```shell
   screen  //直接键入screen命令创建一个空会话 
   exit //退出当前运行的窗口
   screen -ls //列出后台挂起的所有会话
   screen -r <pid> //使用会话的pid恢复到指定的会话中继续之前的工作
   screen -S <name> //创建一个新的会话
   kill -9 <pid> //终结一个会话窗口
   screen -wipe //清除已死亡的会话
   ```

2. 快捷键

   ```shell
   Ctrl + A + D //暂时断开该回话不中断程序连接
   ```

3. 