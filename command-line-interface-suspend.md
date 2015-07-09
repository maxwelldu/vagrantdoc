suspend
==============

**命令:** `vagrant suspend`

这个停止虚拟机比 完整的[关闭](command-line-interface-halt.md) 或者 [销毁](command-line-interface-destroy.md) 有很大的距离.

暂停有效的保存了虚拟机在那个确切的时间点的状态, 所以当你晚点 [恢复](command-line-interface-resume.md)它, 它从那个点立即运行, 比全部重新启动要快.

这将需要额外的磁盘空间存储虚拟机RAM的所有内容, 但是机器不再耗用RAM在你的主机或者CPU, 当它暂停.
