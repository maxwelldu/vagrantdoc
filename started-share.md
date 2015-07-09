分享
=====================

现在我们有了一个Web服务器启动运行着, 可以通过你的机器访问, 我们有了一个功能相当完整的开发环境. 但是另外提供一个开发环境, Vagrant 也可以很容易的分享和合作在他们的环境上. 这个Vagrant上面主要的特性被叫做 [分享Vagrant](vagrant-share-overview.md).

分享Vagrant让你分享你的Vagrant环境给世界上的任何一个人. 它将给你一个可以直接路由到你的Vagrant环境的URL, 从连接到网络的任何设施在这个世界.

登录到 Hashicorp's Atlas
----------------------------

在你能够分享你的Vagrant环境之前, 你需要一个帐号在 [HashiCorp's Atlas](https://atlas.hashicorp.com/). 不用担心, 它是免费的.

当你有一个帐号, 使用 `vagrant login` 来登录:

```
$ vagrant login
Username or Email: mitchllh
Password (will be hidden):
You're now logged in!
```

分享
---------

当你登录以后, 运行 `vagrant share`:

```
$ vagrant share
...
==> default: Your Vagrant Share is running!
==> default: URL: http://frosty-weasel-0857.vagrantshare.com
...
```

你的URL将会不一样, 不用尝试和上面的URL一样. 作为替代的, 拷贝 `vagrant share` 输出的供你在web 浏览器上访问的URL. 它将加载我们之前安装页面的首页.

现在, 修改你的 "index.html" 文件并且刷新URL. 它将被更新! URL是直接路由到你的开发环境, 并且工作在任何被连网的设备在这个世界上.

结束分享会话, 敲 `Ctrl+C` 在你的终端. 你会刷新URL再次验证你的环境不再被分享.

分享Vagrant是相当有能力的不仅仅是简单的HTTP分享. 更多细节请看 [完整的分享Vagrant文档](vagrant-share-overview.md).
