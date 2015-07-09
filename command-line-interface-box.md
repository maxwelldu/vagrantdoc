Box
=============

**命令:** `vagrant box`

这个命令用来管理(添加, 移除等等) [boxes](boxes-overview.md).

这个命令被暴露了主要功能的子命令:
* `add`
* `list`
* `outdated`
* `remove`
* `repackage`
* `update`

Box 添加
===================

**命令:** `vagrant box add ADDRESS`

这个添加box需要给一个Vagrant地址. 这个地址能够是以下三件事之一:
* 一个短名称从[公共分类的多种多样的Vagrant镜像](https://atlas.hashicorp.com/boxes/search), 例如 "hashicorp/precise64".
* 文件路径或者HTTP URL到一个box在[catalog](https://atlas.hashicorp.com/boxes/search). 为HTTP, 基础的认证是被支持的并且`http_proxy`环境变量也是被尊重的. 也支持 HTTPS.
* 一个box文件的直接URL, 这种情况, 你必须指定一个`--name` 标记(看下面)并且更新将不会工作.

如果一个错误发生在下载或者用 Ctrl-C 中断下载, 然后Vagrant会在下载请求的时候尝试恢复下载. Vagrant将仅仅尝试恢复下载在初始化下载后的6个小时之内.

选项
-------
* `--box-version VALUE` - 你想要添加的box版本. 默认会添加最新的版本. 这个值可以是一个确切的版本数字, 例如 "1.2.3" 或者它可以设置一个版本约束. 一个版本约束看起来像 ">=1.0, <2.0".
* `--cacert CERTFILE` - CA使用的被验证的证书. 这个应该被用于远程不包含一个用
