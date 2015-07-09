基础语法
===============

配置
---------------

在你的 Vagrantfile 中配置, 使用｀config.vm.synced_folder` 的方式. 配置的命令用法是非常的简单:

```
Vagrant.configure("2") do |config|
  # other config here

  config.vm.synced_folder "src/", "/srv/website"
end
```

第一个参数是主机上面的目录路径. 如果路径是相对的, 它是相对于项目根目录. 第二个参数必须是绝对路径在虚拟机中共享目录. 这个目录将被创建(递归的, 如果是必须)如果它不存在.

选项
--------------

当配置同步目录的时候你也许可以指定附加的参数选项. 这些选项被列在下面. 更多一些使用这些选项的示例展示的在这个区间下面, 注意 owner/group 示例, 两个附加的选项被逗号分开.

附加的这些选项, 指定同步目录的类型可能允许更多的类型. 看文档为你指定同步目录的类型查看更多详情. 内置的同步目录类型是文档在其他页面可用, 为这些文档导航.

* `create` (布尔值) - 如果是true, 主机地址将被创建, 如果它不存在, 默认是false.
* `disabled` (布尔值) - 如果是true, 这个同步目录将被关闭并且不会被设置. 这个可以被用于以前定义的同步目录或者按条件关闭基础定义的一些表面因素.
* `group` (字符串) - 同步目录的组拥有者. 默认这个将会是 SSH 的用户. 一些目录同步的类型不支持修改组.
* `mount_options` (数组) - 一个额外挂载的选项列表通过 `mount` 命令.
* `owner` (字符串) - 这个同步目录的拥有者. 默认将是 SSH 用户. 一些同步目录类型不支持修改拥有者.
* `type` (字符串) - 同步目录的类型, 如果这个不指定, Vagrant 将为你的环境自动选择最好的目录同步选项. 否则, 你可以指定一个特定的类型, 例如 "NFS".

使它可用
---------------

同步目录是自动安装的当 `vagrant up` 和 `vagrant reload`.

使它不可用
----------------

同步目录可以禁用通过 `disabled` 选项到任何定义的:

```
Vagrant.configure("2") do |config|
  config.vm.synced_folder "src/", "/srv/website", disabled: true
end
```

禁用默认的 `/vagrant` 共享可以完成像以下:

```
config.vm.synced_folder ".", "/vagrant", disabled: true
```

修改拥有者和组
----------------

黑夜, Vagrant挂载同步目录使用 SSH 的用户作为拥有者和组. 有些时候挂载目录使用不同的拥有者和组. 它是可以被这些选项设置的:
```
config.vm.synced_folder "src", "/srv/website", owner: "root", group: "root"
```
