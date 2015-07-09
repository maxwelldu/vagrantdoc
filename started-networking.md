网络
=============

我们有一个Web服务器启动并运行, 有能力修改文件从主机, 并且他们会自动同步到虚拟机. 然而从命令行简单的访问 web 页面还不是很满意. 在这一步, 我们将使用 Vagrant 的网络特性来给我们附加一种从我们主机访问虚拟机的方式.

端口转发
-------------

一种选择是使用端口转发. 端口转发允许你指定通过主机的端口在虚拟机上共享. 这允许你在自己的主机上面访问一个端口, 但是的确有网络交通转发到虚拟机一个指定的端口.

让我们设置一个端口转发, 这样我们可以访问到虚拟机里面的 Apache. 简单的编辑 Vagrantfile, 使它看起来像这样:

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.network :forwarded_port, host: 4567, guest: 80
end
```

运行 `vagrant reload` 或者 `vagrant up` (取决于你的机器已经运行) 这些改变能够被影响.

机器再次运行, 在你的浏览器中访问 http://127.0.0.1:4567. 你应该看到一个 Vagrant 自动安装的Apache正在服务的web 页面.

其他网络
-----------------

Vagrant 也有其他形式的网络, 允许你指定一个静态IP地址来访问虚拟机, 或者桥接的形式访问虚拟机在一个已经存在的局域网中. 如果你有兴趣其他的方式, 请阅读 [网络](networking-overview.md)页面
