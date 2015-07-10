最低限度的Vagrant版本
========================

强制人们使用指定的Vagrant版本需要在Vagrantfile中指定一系列的版本需要. 这将帮助你整合问题, 因为否则有可能使用一个非常旧或者非常新的Vagrant版本.

Vagrant需要的版本应该在Vagrant的顶部配置, 使用 `Vagrant.require_version`:

```
Vagrant.require_version ">= 1.3.5"
```

在以上的情况, Vagrantfile将只加载Vagrant1.3.5或以上的版本.

多个需要也可以配置:

```
Vagrant.require_version ">= 1.3.5", "< 1.4.0"
```
