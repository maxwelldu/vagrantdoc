Box文件格式
===================

过去, boxes仅仅是Virtualbox导出的[tar文件](http://en.wikipedia.org/wiki/Tar_(computing)). 现在Vagrant支持多[提供者](providers-overview.md)和多[版本](boxes-versioning.md), box文件变的稍微更复杂一点.

Box文件制作从Vagrant 1.0.x(VirtualBox导出`tar`文件)开始一直工作到今天. 当Vagrant遇到这类旧的boxes, 它会自动在里面更新为一个新的格式.

今天, 有两种不同的组件.

* Box文件 - 这是一种压缩(`tar`, `tar.gz`, `zip`)文件, 是指定单一的提供者, 能够包含任何东西. Vagrant核心文件从来不使用. 作为替代的他们通过提供者. 所以, 一个VirtualBox box文件和一个VMware box文件是有不同的内容等等.

* Box 目录元数据 - 这是一个JSON文档([HashiCorp's Atlas]()是典型的交互), 具体说明box的名字, 一个描述, 可用的版本, 可用的提供者和URLs来找到一个实际的box文件(下一个组件)来为每个提供者以及每个版本. 如果这个目录元数据不存在, 一个box文件仍然可以被支持添加, 但是将不支持版本和更新.

每个组件的详情在下面都会包含到.

Box 文件
------------------

实际的Box文件需要Vagrant的一部分. 推荐你总是使用元数据文件和一个box文件一起, 但是直接的box文件是支持的由于Vagrant的遗留原因.

Box 文件是使用 `tar`, `tar.gz` 或者 `zip`压缩的. 任何东西可以被压缩, 并且指定每个[提供者](providers-overview.m). Vagrant核心会被解压供以后自己使用.

在压缩文件里面, Vagrant预计有一个 `metadata.json` 文件. 这是一个JSON文件, 和上面的目录元数据完全不相关的组件; 这仅仅是每个box文件里面的一个`metadata.json`(在box文件内部), 然而一个目录元数据JSON文档能够描述相同box的多个版本, 也意味着支持多提供者.

`metadata.json` 必须包含至少一个"provider" 键指定是哪个提供者. Vagrant使用这个来验证box的提供者. 例如, 如果你的box是为VirtualBox提供的, `metadata.json`应该看起来像这样:

```
{
  "provider": "virtualbox"
}
```

如果这里没有`metadata.json`文件或者文件里面不包含一个合法的JSON, 至少有一个"provider"键, 那么Vagrant在添加的过程中会出错, 因为它不能够校验提供者.

其他的键和值添加到metadata里面是没问题的. metadata文件的值在Vagrant里面是不透明的, 插件可以使用它. 在这一点, Vagrant核心不使用这个文件中任何其他的键.

BOX METADATA
------------------------

metadata是一个box可选的组件(但是非常推荐), 因为他支持[版本](boxes-versioning.md), 更新, 多提供者从一个文件, 等等.

```
你不需要手动的制作metadata. 如果你有一个HashiCorp's Atlas的帐号, 你可以在那儿创建boxes, HashiCorp's Atlas会自动的为你创建metadata. 这个文档的格式在这样的. 
```

它是一个JSON文档, 以下面这种结构的方式存在:

```
{
  "name": "hashicorp/precise64",
  "description": "This box contains Ubuntu 12.04 LTS 64-bit.",
  "version": [{
    "version": "0.1.0",
    "providers": [{
      "name": "virtualbox",
      "url": "http://somewhere.com/precise64_010_virtualbox.box",
      "checksum_type": "sha1",
      "checksum": "foo"
    }]
  }]
}
```

如你所看到的, 这个JSON文档可以描述一个box的多个版本, 多提供者, 可以从不同的版本中添加/移除 提供者.

这个JSON文件可以直接通过`vagrant box add`从本地文件系统的一个路径, 或者通过一个URL, Vagrant会安装box中合适的版本. 在这种情况, JSON中`url`键的值也可以是一个文件路径. 
如果有多个提供者可用, Vagrant将询问你想要使用哪一个.

