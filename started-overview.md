开始
=============

Vagrant 开始指南将带你通过第一个 Vagrant 项目, 并且展示 Vagrant 提供的最主要特性的基本用法.

如果你好奇 Vagrant 提供了什么好处, 你应该阅读 [Why Vagrant?](why-vagrant-overview.md).

开始指南将基于 [VirtualBox](http://www.virtualbox.org/) 使用Vagrant, 由于它在每个重要的平台都是免费可用的. 在阅读完指南别忘记 Vagrant 可以工作在 [许多其他提供者](providers-overview.md).

在开始第一个项目之前, 请 [安装最新的 Vagrant 版本](https://docs.vagrantup.com/v2/installation/). 因为我们的开始指南将要使用 [VirtualBox](http://www.virtualbox.org/) 作为我们的提供者, 也请下载好.

```
**喜欢书本的人?** 如果你更喜欢读纸质书, 你也许有兴趣在 [Vagrant: 启动和运行](http://www.amazon.com/gp/product/1449335837/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1449335837&linkCode=as2&tag=vagrant-20), 由 Vagrant 的作者书写, 由 O'Reilly. 发布.
```

启动和运行
=================
```
$ vagrant init hashicorp/precise32
$ vagrant up
```

在运行了以上两个命令, 你将有一个完整运行的虚拟机 Ubuntu 12.04 LTS 32位运行在 [VirtualBox](https://www.virtualbox.org/). 你可以 SSH 进入到这台机器用 `vagrant ssh`, 并且当你完成了这个, 你可以移除所有的痕迹用 `vagrant destroy`.

现在想象每个没有用这个工作过的项目可以很容易的安装.

用 Vagrant, `vagrant up` 是在任何项目中仅仅需要的命令, 来安装每一个需要部署的项目, 并且安装任何网络和同步目录, 所以你可以继续工作从你自己舒适的机器.

接下来的指南将带你安装更多完整的项目, 包含更多 Vagrant 的特性.
