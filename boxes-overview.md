Boxes
================

Boxes是Vagrant环境格式的包. 一个Box可以被任何人在任何支持Vagrant的环境中运行.

`vagrant box` 工具提供了全面的管理box的功能. 你可以读文档在[vagrant box]()命令来获取更多信息.

最简单的方式使用一个box是从[Vagrant box公共可用分类中]()得到. 你也可以添加和分享你自己自定义的box在web站点.

Boxes也支持版本, 所以记得你团队使用的Vagrant可以很容易的更新, 人们创建了可以被推送修复的Boxes, 并且这些修复可以快速的进行沟通交流.

你可以学到关于boxes的所有通过阅读这个页面以及子页面在左侧导航.

发现Boxes
-------------

最容易发现boox的方式是在 [公共vagrant box分类]()中找到一个你需要并匹配的实例. 分类包括主要的基础操作系统, 以及专门的boxes来使你启动并快速的运行LAMP层, Ruby, Python, 等等.

从catalog添加box是非常方便的. 每个box都会教你如何添加它, 但是他们都和下面是一样的格式:

```
$ vagrant box add USER/BOX
...
```

例如: `vagrant box add hashicorp/precise64`. 你也可以快速的安装一个Vagrant环境用 `vagrant init hashicorp/precise64`.
