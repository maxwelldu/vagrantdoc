
# 连接
**命令:** `vagrant connect NAME`

连接命令称赞[共享命令][1]以用于启用访问共享环境。你可以在Vagrant共享节查阅有关Vagrantfong共享的详情。

下面的是这个命令可用的命令行标志的参考。

### 选项
* `--disable-static-ip` - 连接命令不会自旋向上一个小虚拟机以创建你能访问的静态IP。当设置了这个标志，访问连接的唯一办法是使用外部的SOCKS代理地址。

* `--static-ip IP` - 告诉虚拟机连接使用的静态IP地址。默认地，Vagrant连接会使用172.16.0.0/16之间可用的IP地址。

* `--ssh` - 通过SSH连接到一个通过`vagrant share --ssh`共享的环境。

[1]: /v2/cli/share
[2]: /v2/share/
