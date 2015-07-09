网络的基础用法
===================

Vagrant 为你如何能够连接到你的虚拟机网络提供了多种方式, 但是有一个标准的模式和许多我们知道重要的通用的通用网络配置.

配置
-----------------

所有的网络在你的 [Vagrantfile](vagrantfile-overview.md) 中配置, 用 `config.vm.network` 方法调用. 例如, 以下的 Vagrantfile 定义了端口转发:

```
Vagrant.configure("2") do |config|
  # other config here

  config.vm.network "forwared_port", guest: 80, host: 8080
end
```

每一种网络类型有一个唯一标识, 例如以上面例子中的 `:forwarded_port`. 接下来有一系列的配置参数可以区别于每一种网络类型. 在端口转发的情况, 需要填写两个数字参数: 在虚拟机中可以被访问的端口, 和主机上配置的一个端口.

多个网络
-------------

多个网络可以在 Vagrantfile 中定义多个 `config.vm.network`. 确切的说可以区别于每个[提供者](providers-overview.md), 但是通常情况为了指定网络是可用的.

使网络生效
-------------

网络会自动配置并且可用当他们被定义在 Vagrantfile 中, 作为 `vagrant up` 或者 `vagrant reload` 进程的一部分.


