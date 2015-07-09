环境变量
===============

Vagrant有一系列的环境变量以致于能够被配置文件使用并且用全局的方式控制. 这个列出了这些环境变量.

VAGRANT_CHECKPOINT_DISABLE
---------------------------

Vagrant有时候会访问网络检查Vagrant当前运行的版本是最新的. 我们都理解软件会通过网络制造一些远程调用, 不管是什么原因都是不受欢迎的, 为了限制这些调用, 设置环境变量 `VAGRANT_CHECKPOINT_DISABLE` 为任何不为空的值.

VAGRANT_CWD
--------------------

`VAGRANT_CWD`可以被设置用来改变Vagrant的工作目录. 默认的, Vagrant使用你在的当前目录. 工作目录是重要的, 因为它是Vagrant从哪儿开始找Vagrantfile. 它也定义了相对路径在Vagrantfile中是扩展, 由于他们使用相对路径是在Vagrantfile所在位置开始找.

这个环境变量是最通用的设置能够从一个脚本环境运行Vagrant为了设置目录让Vagrant能够看到. 

VAGRANT_DOTFILE_PATH
------------------------

`VAGRANT_DOTFILE_PATH`能够被设置来改变Vagrant存储的虚拟机的状态目录, 例如虚拟机的UDID. 默认, 这个被设置为`.vagrant`. 如果你保持你的Vagrantfile在一个Dropbox目录为了分享文件在桌面和笔记本(举例), Vagrant将在这个目录重写虚拟机的详细信息在最近使用的主机上面. 要避免这样, 你可以设置`VAGRANT_DOTFILE_PATH`到`.vagrant-laptop` 和 `.vagrant-desktop` 在各自机器上面. (记得更新你的`.gitignore`!)

VAGRANT_HOME
----------------------

`VAGRANT_HOME`可以被设置来改变Vagrant存储的全局的状态. 默认被设置为`~/.vagrant.d`. 这个Vagrant家目录是boxes被存储的位置, 所以它的确需要在磁盘上变的相当大.

VAGRANT_LOG
----------------------

`VAGRANT_LOG` 详细的说明Vagrant的日志. 默认Vagrant不会主动的显示任何日志消息.

日志消息是非常有用的当分析解决问题的时候, 提交Bugs, 或者得到支持. 在大多数冗长的等级, Vagrant输出基本上每件它正在做的事情.

可用的日志等级是 "debug", "info", "warn", 和 "error". "warn" 和 "error" 几乎没有用, 由于 他们很少会发生, Vagrant通常会报告他们在一个标签的输出.

"info" 是一个很好的等级来开始, 如果你有问题, 因为当相当大超过正常输出, 它仍然是人们可读并且能够帮助识别确定的问题.

"debug" 输出是非常冗余的, 并且很难阅读没有一些Vagrant的内部知识. 然而最好的输出是支持请求, 或者bug举报.

VAGRANT_NO_COLOR
-------------------------

如果这个被设置为任何值, 那么Vagrant将不会使用任何颜色输出. 这是一个非常有用的, 如果你正在输出一个文件或一个系统不支持颜色.

这个行为能够被实现通过使用`--no-color` 标记在命令行. 这个环境变量是非常有用的全局设置标记.

VAGRANT_NO_PLUGINS
--------------------------

如果这个设置为任何值, 那么Vagrant将不加载任何第三方插件. 这个非常有用如果你安装了插件, 它是介绍Vagrant的不稳定, 或者如果你想指定一个Vagrant环境不加载插件.

注意任何`vagrant plugin` 命令自动的不加载任何插件, 所以如果你安装任何不固定的插件, 你可以总是使用`vagrant plugin` 命令不需要担心.

VAGRANT_VAGRANTFILE
----------------------------

这个指定Vagrant搜索的Vagrantfile的文件名. 默认的这个是 "Vagrantfile". 注意这不是一个文件路径, 仅仅是一个文件名.

这个环境变量通常被用于脚本环境当一个文件能够包含多个Vagrantfile代表不同的环境.
