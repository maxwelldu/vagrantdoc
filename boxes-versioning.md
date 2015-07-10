Box 版本
==================

从Vagrant1.5起, boxes支持版本. 这就允许人们制作boxes来推送更新box, 使用的人只需要简单的检查更新, 然后更新他们的boxes, 看看改变了什么. 

如果你只是刚刚开始用Vagrant, box版本不是太重要, 我们推荐你先学习一些其他的主题, 但是如果你在团队中使用Vagrant或者计划制作你自己的boxes, 版本是非常重要. 很幸运, 正确的建立版本让Vagrant更容易使用, 更愉快的使用Vagrant工作.

这一页将包含如何使用有版本的boxes. 不包含如何更新你自定义的boxes版本. 在这一节会包含[创建一个box](boxes-create-a-base-box.md).

查看版本并更新
-------------------------

`vagrant box list` 仅显示安装过的boxes版本. 如果你想要看全部可用的box版本, 你就必须在[HashiCorp's Atlas](https://atlas.hashicorp.com/)上面找到box. 一种更容易找到一个box的方式是使用url `https://atlas.hashicorp.com/USER/BOX`. 例如找 `hashicorp/precise64` 这个box, 你可以在`https://atlas.hashicorp.com/hashicorp/precise64` 找到信息.

你可以用`vagrant box outdated` 检查过时的box.
这也可以简单你当前的Vagrant环境是否过期, 以及系统上安装的其他box.

最后, 你可以用`vagrant box update`更新boxes. 这将下载和安装新的box. 这不会魔法般的更新正在运行的Vagrant环境. 如果一个Vagrant环境已经准备运行. 你将必须销毁并且用box里面新更新的版本重新创建. 更新命令就是下载这些本地的更新.

版本限制
-----------------------

你可以限制你的Vagrant环境为一个指定的版本或者一个box的版本, 使用 [Vagrantfile](vagrantfile-overview.md)指定`config.vm.box_version` 选项.


如果这个选项没有指定, 则总是会使用最新的版本. 这等于指定一个约束 ">=0".

box版本配置可以是指定一个版本或者限制版本.
限制可以是以下任意的组合: `= X`, `>X`, `< X`, `>= X`, `<= X`, `~> X`. 你可以使用多种组合使用, 用逗号分隔.

所有的约束应该解释自己, 除了`~>` 之外, 这是一个悲观的约束. 举例说明最好: `~> 1.0` 等于 `>=1.0, <2.0`. `~> 1.1.5` 等于 `>=1.1.5, < 1.2.0`.

你可以手动选项你看见合适的版本. 然而, 许多公共分类的boxes都遵循[语义版本](http://semver.org/). 基本上, 只有第一个数字(重要的版本)打破向后兼容. 这通常意味着任何能运行在"1.1.5"版本的box都可以运行在 "1.2", "1.4.5"等版本. 但是 "2.0" 可能介绍巨大的改变会打破你的软件. 根据这个, 最好的约束是`~> 1.0`, 因为你知道它是安全的, 在这个区间不用担心.

当然, 随你喜欢, 你是免费的使用版本.

自动更新检查
-------------------------

使用[Vagrantfile](vagrantfile-overview.md), 你也可以配置Vagrant自动检查更新在任何`vagrant up`的时候. 这是默认开启的, 但是可以很容易的禁止通过配置文件里面设置`config.vm.box_check_update = false`.

当这是可用的, Vagrant将会检查更新当每次`vagrant up`的时候, 不仅仅是当机器被从远程创建的时候, 也包括恢复, 关机之后的开启等等.

如果一个更新被找到, Vagrant将会输出一个警告来rjfietyn知道有可用的更新. 用户可以选择暂时忽略警告, 或者可以使用`vagrant box update`来更新box.

Vagrant不可以也不能自动下载更新的box来更新机器, 因为boxes是相当大, 更新机器需要销毁它并且重新创建, 会导致重要的数据丢失. 所以需要用户手动输入一个命令来完成这个操作.

裁剪旧版本
--------------------------

Vagrant不会自动删除旧版本, 因为他不知道他们是否有可能被另外的Vagrant环境使用. 因为boxes很大, 你可能想要主动的删除它通过`vagrant box remove`. 你可以看到所有已经安装的boxes通过`vagrant box list`.

