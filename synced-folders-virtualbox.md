VirtualBox
============

如果你在使用 VirtualBox 作为[提供者](https://docs.vagrantup.com/v2/providers/), 那么 VirtualBox 分享目录是默认的同步目录类型. 这些同步的目录使用 VirtualBox 从虚拟机到主机分享目录系统来同步文件改变.

警告
-------------

这是一个 [VirtualBox bug](https://github.com/mitchellh/vagrant/issues/351#issuecomment-1339640) 关联到不好的结果或者没有更新文件 `sendfile`. 你应该关闭 `sendfile` 在任何你运行的 web服务器.

在Nginx中:

```
sendfile off;
```

在Apache中:

```
EnableSendfile Off
```
