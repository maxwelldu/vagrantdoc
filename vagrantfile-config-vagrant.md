Vagrant配置
================

**配置命令空间:** `config.vagrant`

用`config.vagrant` 来修改Vagrant自身的表现.

可用的设置
--------------------

`config.vagrant.host` - 这个设置正在运行的主机类型. 默认这个是 `:detect`, 因为Vagrant会自动发现主机. Vagrant需要知道更多信息为了指定主机的一些事情, 例如准备用NFS目录, 如果他们可用. 你应该只能手动设置这个如果自动发现失败的话.
