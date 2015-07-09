Boxes
=============

代替传统的建立一个虚拟机, 它是一个慢速和乏味的过程, Vagrant 用一个基础镜像来快速克隆一个虚拟机.
这些基础镜像在 Vagrant 中被称为 boxes, 并且为你的 Vagrant 环境总是在你创建一个新的 Vagrantfile 后的第一步来指定具体使用哪个box.

安装一个 Box
----------------

如果你运行过命令根据 [快速开始](started-overview.md), 那么你之前已经安装了一个box, 你不需要再次运行以下命令. 
然而这段仍然是值得阅读的来学习更多关于如何管理 boxes.

Boxes 是用 `vagrant box add` 添加到 Vagrant上面. 这个用指定了名字存储, 所以许多 Vagrant 环境可以重用它. 如果你还没有添加一个 box, 你现在可以这样做:

```
$ vagrant box add hashicorp/precise32
```

这个将从 [HashiCorp's Atlas box catalog](https://atlas.hashicorp.com/boxes/search) 下载一个名字为 "hashicorp/precise32" 的 box, 你可以从这个地址找到 boxes. 从 HashiCorp's Atlas 下载是相当容易的, 当然你也可以添加 boxes 从本地文件, 自定义 URL, 等等.

添加 boxes 可以被多个项目重用. 每个项目使用一个 box 作为初始化镜像来克隆, 并且从来不会修改实际的基础镜像. 这意味着如果你有两个项目都在使用我们刚刚添加的 `hashicorp/precise32` box, 从一台虚拟机上面添加文件将不会影响其他的机器.

使用一个 Box
------------------

现在上面的 box 已经被添加到 Vagrant, 我们需要配置我们的项目来使用它作为基础. 打开 `Vagrantfile` 并且修改内容如下:

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
end
```

"hashicorp/precise32" 在这种情况必须匹配你上面添加的 box 的名字. 这是让 Vagrant 知道应该使用哪个 box. 如果 box 之前没有被添加, Vagrant 将会自动下载并且添加 box 当它运行.

在下一节, 我们会带来 Vagrant 环境和交互用它.

找到更多 Boxes
---------------------

为了剩下的开始指南, 我们将只使用我们之前添加的 "hashicorp/precise32" box. 但是完成开始指南不久, 你的第一个问题可能是 "我到哪里找到更多的 boxes?"

找到更多boxes 最好的地方是 [HashiCorp's Atlas box catalog](). HashiCorp's Atlas 有一个公众的免费可能的 boxes 目录, 可以运行在许多平台. HashiCorp's Atlas也有一个强大的搜索特性允许你来找到你关心的 box.

另外的方式找到免费的 boxes, HashiCorp's Atlas 让你管理自己的 boxes, 如果你想要使用一个私有的 box, 可以在你自己的组织下面创建 boxes.
