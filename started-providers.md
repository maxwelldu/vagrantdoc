提供者
================

在这个开始指南, 你的项目总是运行在 [VirtualBox](http://www.virtualbox.org/). 但是Vagrant 可以运行在多种多样的提供者上面, 例如 [VMware](https://docs.vagrantup.com/v2/vmware/), [AWS](http://github.com/mitchellh/vagrant-aws), 还有更多. 更多关于如何建立它们的信息在每一个 提供者页面.

我们已经安装了一个提供者, 你不需要做任何的修改在你的 Vagrantfile, 仅仅 `vagrant up` 会使用一个适当的提供者并且 Vagrant 将会做其余的事情:

```
$ vagrant up --provider=vmware_fusion
...
```

准备好移动到云? 带它到 AWS:

```
$ vagrant up --provider=aws
...
```

以上是你运行 `vagrant up` 使用另外的提供者, 每一个其他的 vagrant 命令不需要你告诉它应该使用哪个提供者. Vagrant 会自动识别出来. 
所以当你准备 SSH 或者 销毁 或者其他的任何情况, 仅仅运行命令像正常的一样, 例如 `vagrant destroy`. 没有必要输入额外的标记.

更多关于提供者的信息, 请阅读完整的文档在 [提供者](providers-overview.md)
