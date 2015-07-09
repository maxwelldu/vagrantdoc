提供
==================

好了, 我们有了一个运行 Ubuntu 镜像的虚拟机, 我们也可以从我们的机器编辑文件, 它会自动同步到虚拟机. 让我们用 web 服务器服务更多文件.

我们可以只通过 SSH 进入, 然后安装一个 web 服务器用我们自己的方式, 但是每个使用Vagrant的人将必须做相同的事情. 作为替代的, Vagrant 有一个内部支持的自动提供. 使用这个特性, Vagrant 将自动安装软件当你 `vagrant up`, 所以虚拟机可以被重建然后准备使用.

安装 Apache
-------------------

我们将为我们的基础项目仅仅安装 [Apache](http://httpd.apache.org/), 我们将使用一个 shell 脚本来做这事.
创建以下的脚本然后保存为 `bootstrap.sh`, 存放在和 Vagrantfile 相同的目录:

```
#!/usr/bin/env bash

apt-get update
apt-get install -y apache2
if ! [ -L /var/www ]; then 
  rm -rf /var/www
  ln -fs /vagrant /var/www
fi
```

接下来我们配置 Vagrant 在安装我们的虚拟机的时候来运行这个 shell 脚本. 我们通过编辑 Vagrantfile来完成, 使它看起来像以下:

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provision :shell, path: "bootstrap.sh"
end
```

"provision" 这一行是新的, 是告诉 Vagrant 来使用 `shell` 提供者来安装机器, 用 `bootstrap.sh` 文件 . 这个文件路径是相当于 项目根目录(Vagrantfile所在的目录).

提供
---------------

在配置完成后, 仅运行 `vagrant up` 来创建你的机器, Vagrant 会自动的服务. 你应该看到shell脚本的输出出现在你的命令行, 如果虚拟机已经从服务中运行, 运行 `vagrant reload --provision` 将会快速的重启你的虚拟机, 跳过初始化导入的步骤. 服务标记在重启命令指导 Vagrant 运行服务, 由于Vagrant 将只会在第一次 `vagrant up`的时候.

Vagrant 完整运行完成之后, web 服务将会启动和运行, 你现在还不能在自己的浏览器中看到 web 站点, 但是可以核对服务是否工作, 通过虚拟机里面的 SSH 加载一个文件:

```
$ vagrant ssh
...
vagrant@precise32:~$ wget -q0- 127.0.0.1
```

这个会有效, 因为在以上的 shell 脚本我们安装了Apache并且设置了默认的 `DocumentRoot` 为我们的 `/vagrant` 目录, 就是Vagrant 默认同步的目录.

你可以创建更多的文件并且浏览他们在命令行, 但是在下一步我们将会包含网络选项, 所以你会使用浏览器访问你的虚拟机.
