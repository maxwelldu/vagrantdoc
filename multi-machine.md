多台主机
================

Vagrant是可以定义和控制多台虚拟机在每个Vagrantfile中. 这个被我们称作 "多机器" 环境.

这些机器通常能够一起工作或者以某种方式相互关联. 这里有一些实例关于人们今天在使用多机器环境:

* 解剖一个很清晰的多机器模型, 例如将Web服务器和数据库服务器分开.
* 分布式系统模型他们是如何相互交互.
* 测试一个接口, 例如一个API到服务组件.
* 灾难用例测试: 机器宕机了, 网络隔离, 网络慢, 不一致的视图等等.

历史上, 运行复杂的环境, 例如把这些都放到一个单一的机器. 问题是它是一个不准确的模型, 他的表现差距很大.

使用Vagrant 的多机器特性, 这些环境能够被制造在一个单一的Vagrant环境而不会丢失Vagrant的优点.

定义多机器
----------------

多机器用`config.vm.define`方式被定义在相同的项目 [Vagrantfile](vagrantfile-overview.md). 这个配置命令有一点点好玩, 因为它在一个配置中创建一个Vagrant配置. 下面这个是最好的例子:

```
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "web" do |web|
    web.vm.box = "apache"
  end

  config.vm.define "db" do |db|
    db.vm.box = "mysql"
  end
end
```

如你所见, `config.vm.define` 和其他的变量占用了一块. 这个变量, 例如上面的 `web`, 是准确的和`config`的变量一样, 除一行中应用的任何配置只被定义. 所以任何配置在 `web` 将只会影响 `web` 机器.

重要的是你可以继续使用`config`对象. 配置对象被加载和合并在指定的机器配置之前, 就像其他 Vagrantfile 在 [Vagrant load order](vagrantfile-overview.md)一样.

如果你对程序比较熟悉, 这个类似于语言有不同的变量作用域.

当使用这些作用域, 事情的执行顺序例如提供者们变的比较重要. Vagrant 强制从外到内排序, 在Vagrantfile的列表排序. 例如以下的Vagrantfile:

```
Vagrant.configure("2") do |config|
  config.vm.provision :shell, inline: 'echo A'
  config.vm.define :testing do |test|
    test.vm.provision :shell, inline: 'echo B'
  end
  config.vm.provision :shell, inline: 'echo C'
end
```

提供者在这种情况将会输出A, 然后是C, 然后是B. 提示B是最好. 是因为排序是从外到内的, 在文件的排序.

控制多台机器
--------------

现在在一个Vagrantfile中定义超过一台机器, 许多`vagrant` 的命令稍微有点改变. 改变凭直观感觉.

命令能够感觉到一个目标, 例如 `vagrant ssh`, 现在需要机器的名字来控制. 使用以上示例, 你应该用 `vagrant ssh web` 或者 `vagrant ssh db`.

其他命令, 例如 `vagrant up`, 默认会在每台机器上面操作. 所以如果你运行 `vagrant up`, Vagrant将把web和db机器一起启动. 你也可以有选择的指定, `vagrant up web` 或者 `vagrant up db`.

另外, 你可以指定一个正则来匹配确定的机器. 这个在你指定了许多相似的机器时非常有用, 例如, 如果你测试一个分布式的服务, 你可能有一个`leader` 服务器以及一台`follower0`, `follower1`, `follower2`, 等等. 如果你想要启动所有的followers但是不启动leader, 你可以仅仅这样做 `vagrant up /follower[0-9]/`. 如果Vagrant看见一个机器的名称有斜线, 它会假设你正在使用一个正则表达式.

在机器之间交流
-----------------

为了加载机器之间的交流在安装多机器的环境中, 许多[网络](networking-overview.md)选项可以被用, 特指[私有网络](networking-private-network.md)可以被用来制作一个私有网络在多台机器和主机之间.

具体说明一个主要的机器
------------------------

你也可以指定一个主要的机器. 主要的机器将作为默认机器使用当没有指定机器在多机器环境中.

指定一个默认的机器, 只需要在定义它的时候标记他是 primary. 只能指定一台主要的机器.

```
config.vm.define "web", primary: true do |web|
  # ...
end
```

自动启动机器
----------------

在多机器环境中默认情况下, `vagrant up` 将会启动定义的所有机器. `autostart` 设置允许你告诉Vagrant不启动指定的机器. 例如:

```
config.vm.define "web"
config.vm.define "db"
config.vm.define "db_follower", autostart: false
```

当你使用以上的设置运行 `vagrant up`, Vagrant 将会自动启动 "web" 和 "db" 机器, 但是它不会启动 "db_follower" 机器. 你可以手动运行 `vagrant up db_follower` 来强制启动 "db_follower" 机器.
