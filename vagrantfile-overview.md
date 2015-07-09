Vagrantfile
====================

Vagrant主要的功能是描述项目所需要的机器的类型, 并且如何配置和提供这些机器. Vagrantfile 被称为 Vagrantfile 是因为实际的字面文件名为文件是 `Vagrantfile` (除非你无关紧要的文件系统运行在严格区分大小写的模式).

Vagrant是每个运行的项目带有一个Vagrantfile, 并且Vagrantfile被认为应该提交到版本控制里面. 这将允许其他的开发者在检出项目代码时需要, 运行`vagrant up`, 并用他们的方式, Vagrantfile 是方便穿越每个支持Vagrant的平台.

Vagrantfile的语法是 [Ruby](), 但是修改Vagrantfile没必要拥有Ruby程序语言的知识, 由于它大部分都是很简单的变量赋值. 事实上, Ruby 甚至不是最受欢迎的社区在Vagrant的使用, 这将有助于你表明, 尽管没有红宝石的知识, 人们在Vagrant上面还是很成功的. 

查找路径
----------------

当你运行任何`vagrant`命令, Vagrant 在你的目录不断向上查找第一个能够找到的 Vagrantfile, 在当前目录开始第一个. 所以如果你运行`vagrant`在`/home/mitchellh/projects/foo`, 它将查找顺序查找以下路径找一个Vagrantfile, 直到它找到一个:

```
/home/mitchellh/projects/foo/Vagrantfile
/home/mitchellh/projects/Vagrantfile
/home/mitchellh/Vagrantfile
/home/Vagrantfile
/Vagrantfile
```

这个特性让你运行`vagrant`从你项目中的任意目录.

你可以改变Vagrant查找Vagrantfile的第一个目录通过设置`VAGRANT_CWD`环境变量到一些其他的路径.

加载顺序并且合并
-------------------

一个重要的概念来理解Vagrant是如何加载Vagrantfile的. Vagrant实际上加载一系列的Vagrantfiles, 并且设置. 这将允许Vagrantfile 推倒之前不同等级的配置. Vagrantfiles 被从上到下的顺序加载. 注意在任何一步没找到Vagrantfile, Vagrant将继续下一步.

1. Vagrantfile 被box打包, 被用于指定机器.
2. Vagrantfile 在你的Vagrant家目录(默认在`~/.vagrant.d`). 这使你指定一些默认为你的系统用户.
3. Vagrantfile 来自项目目录. 这是大多数时间你会修改Vagrantfile.
4. 多机器优先.
5. 提供指定的优先.

在每个等级, 设置将会被之前的值合并. 这确切的意味着依赖于设置. 对于大多数设置, 这意味着较新的设置覆盖旧的. 然而, 对于例如定义网络, 网络的确被追加在每一个其他的后面. 默认, 你应该假定那些配置将被相互覆盖. 如果表现不同, 它将会提示有关的文档区间.

在每一个Vagrantfile中, 你可能指定多个`Vagrant.configure` 块. 所有的配置将被合并成一个单独的Vagrantfile 根据他们定义的排序.

可用的配置选项
------------------

你可以学习更多关于变量配置选项通过点击相关区间在左边导航区域.
