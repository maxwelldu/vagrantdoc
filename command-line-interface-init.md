Init
=============

**命令:** `vagrant init [盒子名称] [盒子URL]

这个命令会在当前目录下载初始化Vagrant环境, 通过创建一个初始化[Vagrantfile]() 如果没有一个存在.

如果提供第一个参数, 它会预设置 `config.vm.box` 在被创建的Vagrantfile中. 

如果提供第二个参数, 它会预设置 `config.vm.box_url` 在被创建的Vagrantfile中.

选项
------------

* `--force` - 如果指定, 这个命令将会重写任何存在的 `Vagrantfile`.
* `--minimal` - 如果指定, 一个最小化的Vagrantfile 将会被创建. 这个Vagrantfile 不包含教学注释, 一个正常的Vagrantfile 会包含.
* `--output FILE` - 这将会输出Vagrantfile为指定的文件. 如果这个是"-", Vagrant会被发送到标准输出. 
