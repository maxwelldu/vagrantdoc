公共网络
===============

**网络标识:** `public_network`

公共网络没有私有网络那么私有, 确切的不同来自于[提供者到提供者](providers-overview.md), 因此是模棱两可的定义. 想法是当[私有网络](networking-private-network.md)应该从来不被允许公共的方式访问你的机器, 公共网络可以. 

```
疑惑? 我们也是. 它像公共网络被 :bridged 代替在将来发布, 由于这个通常应该被公共网络完成, 并且提供者通常不支持桥接任何其他特性映射到公共网络.
```

```
警告: Vagrant boxes默认是不肯定的, 根据设计, 特性, 公共密码, 不自信的通过密钥访问, 并且有潜在的允许root通过SSH访问. 我们知道这些, 你的box是在网络中更容易访问. 配置Vagrant之前用一个公共网络, 考虑所有潜在的安全和检查 [默认box配置](boxes-create-a-base-box.md) 来识别潜在的安全风险.
```

DHCP
-------------

更简单的方式使用一个公共网络是通过动态主机配置协议分配一个IP. 
在这种情况下, 定义一个公共网络是太简单不过了:

```
Vagrant.configure("2") do |config|
  config.vm.network "public_network"
end
```

当 DHCP 被使用, IP可以被查看到, 通过 `vagrant ssh` 连接到虚拟机里面, 使用合适的命令行工具来查找IP, 例如 `ifconfig`.

静态IP
----------------

取决于你的配置, 你可能希望手动设置你的IP为桥接模式. 要这样做, 添加一 `:ip` 分句到网络定义.

```
config.vm.network "public_network", ip: "192.168.0.17"
```

默认的网络接口
------------------

如果超过一个可用的网络接口在主机上面, Vagrant将询问你选择哪个接口在虚拟机进行桥接. 一个默认的接口可以指定通过添加一个 `:bridge` 分句在网络定义:

```
config.vm.network "public_network", bridge: 'en1: Wi-Fi (AirPort)'
```

这个字符串标识确切的希望的接口名字, 名字必须要是一个可用的接口. 如果它不能找到, Vagrant 将询问你从可用的网络接口当中挑选一个.
