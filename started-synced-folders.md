同步目录
=============

当它很酷的拥有一个虚拟机是如何容易, 不是很多人想要通过SSH的命令行编辑文件. 很幸运的是你不需要. 通过使用同步目录, Vagrant 将自动同步你的文件到访问的机器.

默认的, Vagrant 分享你的项目目录(记住, 是 Vagrantfile 所在的目录) 到 `/vagrant` 目录在你访问的机器. 再次运行 `vagrant up`, 并且SSH进入到机器查看:

```
$ vagrant up
...
$ vagrant ssh
...
vagrant@precise32:~$ ls /vagrant
Vagrantfile
```

相信它或者不相信, 你看到在虚拟机里面的那个 Vagrantfile 的确和你真实的机器上面的 Vagrantfile 是一样的. 自己继续创建一个文件来证明:

```
vagrant@precise32:~$ touch /vagrant/foo
vagrant@precise32:~$ exit

$ ls
foo Vagrantfile
```

哇哦! "foo" 现在在你的真实机器上面. 如你所见, Vagrant 保持了目录在同步.

看 [同步目录](synced-folders-overview.md), 你可以继续用你的机器上编辑, 并且将文件同步到访问的机器上面. 
