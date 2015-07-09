私有网络
================

**网络标识:** `private_network`

私有网络允许你访问你的虚拟机通过一些地址访问, 但是不能在整个网络中访问. 通常, 这意味着你的机器得到一个地址在[私有地址空间](http://en.wikipedia.org/wiki/Private_network#Private_IPv4_address_spaces)

多台机器使用同样的私有网络(也通常被限制运行在相同的[提供者](providers-overview.md)) 能够每一个其他的私有网络交流.

```
虚拟机操作系统支持. 私有网络通常配置网络适配器在虚拟机上面. 这个过程与操作系统到操作系统之间不同. Vagrant 船有如何配置网络的知识在一个多样化的虚拟机操作系统上面, 但是私有网络可能不会正确的配置当你使用一个特定旧的或新的操作系统.
```

动态主机配置协议
-------------------

最简单的方式使用私有网络是允许自动分配IP通过动态主机配置协议.

```
Vagrant.configure("2") do |config|
  config.vm.network "private_network", type: "dhcp"
end
```

这将自动分配IP地址从储备的地址池. IP地址能够被查到, 通过用 `vagrant ssh` 连接到虚拟机, 使用合适的命令行工具来查找IP, 例如 `ifconfig`.

静态IP
--------------------

你也可以为虚拟机指定一个静态的IP地址. 你将使用静态的已知的IP地址访问 Vagrant 管理虚拟机. Vagrantfile 配置静态IP看起来像这样:

```
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.50.4"
end
```

静态IP地址取决于用户确定在同样的网络中没有其他的机器冲突.

你可以选择你喜欢的任意的IP, 你应该使用IP从[保留的私有网络空间](). 这些IP地址通常从来不会被公共路由到, 并且大多数路由确实限制了网络从外面的世界连接.

不允许自动配置
--------------------

如果你想自己手动配置网络, 你可以禁止 Vagrant 的自动配置特性通过 具体的 `auto_config`:

```
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.50.4",
  auto_config: false
end
```
