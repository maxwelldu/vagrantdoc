提供者基本用法
====================

boxes
--------------------

boxes是所有的具体提供者. 一个VirtualBox的box和VMware的提供者之间是有冲突的, 或者任何其他的提供者. 一个box必须为每种提供者安装, 可以分享同样的名字为其他的box只是提供者不一样. 所以你可以同时拥有 VirtualBox 和 VMware Fusion的 "precise64" box.

安装boxes一点都没有改变:

```
$ vagrant box add \
precise64 http://files.vagrantup.com/precise64.bx
```

Vagrant会自动检查这个box是哪个提供者提供. 在box清单里面是可以查看到的. Vagrant放了提供者在名字后面的括号中, 如下所见.

```
$ vagrant box list
precise64 (virtualbox)
precise64 (vmware_fusion)
```

Vagrant up
------------------

当一个提供者被安装, 你可以使用`vagrant up`命令带上`--provider`标记. 这将强制Vagrant来使用指定的提供者. 不必要配置其他的.

在正常的使用中, `--provider` 标记是不必要的, 自从Vagrant能够为你挑选合适的提供者. 更多细节请看下面介绍.

```
$ vagrant up --provider=vmware_fusion
```

如果你指定了一个 `--provider` 标记, 你仅需要做这个为`up`命令. 机器一旦启动和运行, vagrant就能看见是哪个提供者在后台运行机器, 所以命令例如`destroy`, `suspend`, 等等. 不再需要告诉Vagrant该使用哪个提供者.

```
限制
Vagrant当前会限制你启动一个提供者的每台机器. 如果你有一个多机器环境, 你可以一个使用VirtualBox, 另外一个使用VMware Fusion, 例如, 但是你不可以在VirtualBox和VMwareFusion里面运行同一台机器.
```

默认的提供者
------------------

提早提到, 你可能从来不需要指定 `--provider`. Vagrant是聪明的足够判断你想要用哪个提供者提供环境.

Vagrant尝试找到一个默认的提供者, 按照以下顺序:
1. `--provider` 标记在`vagrant up`的时候其余的会全部选择对应的, 如果存在.
2. 如果 `VAGRANT_DEFAULT_PROVIDER`环境变量被设置, 它将下一个优先选择提供者.
3. Vagrant会通过Vagrantfile中所有的`config.vm.provider`调用来尝试排序. 它将选择第一个可用的提供者. 例如, 你配置了 Hyper-V, 这种方式将从来不会在Mac上面选择. 它必须被配置, 并且可用.
4. Vagrant将会通过安装的提供者插件(包括来自Vagrant的), 并且找到第一个可用的插件. 在这里是系统优先: 系统知道哪个优先级更高, 哪个更糟. 例如, 如果你安装了VMware提供者, 他的优先级高于VirtualBox.
5. 如果Vagrant仍然没找到任何可用的提供者, 它会出错. 

使用这种方式, 将会很少有情况找不到一个正确的提供者给你. 这也允许每个[Vagrantfile](vagrantfile-overview.md)来定义开发环境是使用哪个提供者为配置排序.

在你的Vagrantfile顶部没有定义你想要的排序支持可以使用 `config.vm.provider`:

```
Vagrant.configure("2") do |config|
  # ... other config up here

  # Prefer VMware Fusion before VirtualBox
  config.vm.provider "vmware_fusion"
  config.vm.provider "virtualbox"
end
```
