项目安装
===========

所有使用 Vagrant的项目的第一步是用 [Vagrantfile](vagrantfile-overview.md) 配置Vagrant. Vagrantfile 有以下两个目的:

1. 标记你项目的根目录. 许多 Vagrant 的配置是关联到根目录的. 

2. 描述了机器的类型和你运行你项目所需要的资源, 以及你需要安装的软件以及你想如何访问它.

Vagrant 在一个目录里面初始化的命令是: `vagrant init`. 为了这个指南的目标, 请输入以下命令在你的命令行:

```
$ mkdir vagrant_getting_started
$ cd vagrant_getting_started
$ vagrant init

```

这将放一个 `Vagrantfile` 在你的当前目录. 你可以看一下 Vagrantfile, 如果你想, 内容是注释和示例. 不要害怕如果它看起来恐怖, 我们很快就会修改它.

你可以运行 `vagrant init` 在一个已经存在的目录为已存在的项目安装 Vagrant.

如果你在使用版本控制, Vagrantfile 应该被提供到你的版本控制和你的项目一起. 这种方式, 每个使用那个项目工作的人可以从 Vagrant 感受到好处, 而不需要上面的工作.


