配置版本
================

配置版本是Vagrant1.1以上可用, 并保持[向后兼容](install-backward-compatibility.md), 使用 Vagrant1.0.x的Vagrantfiles, 当推荐新特性和配置作为可选的.

如果你今天运行`vagrant init`, Vagrantfile的格式将会大致如下:

```
Vagrant.configure(2) do |config|
  # ...
end
```

第一行的 `"2"` 相当于配置的对象 `config`, 将被用于配置这个块(在`do` 和 `end`的区间). 这个对象在版本和版本之间是不相同的.

当前, 仅支持两个版本: "1" 和 "2". 版本1相当于配置Vagrant1.0.x. "2" 相当配置 1.1以上以及2.0.X以上.

当加载Vagrantfiles, Vagrant为每个对象使用合适的配置, 就像任何其他的配置一样正确的合并它们.

作为普通用户理解最重要的事情是在一个单独的配置区间, 当单独的一个版本能够被使用. 你将不会使用新的`config.vm.provider` 配置在一个版本1的配置区间. 同样的, `config.vm.forward_port` 将不会在版本2配置区间生效(它被重命名).

如果你想, 你可以合并多个版本配置在同一个Vagrantfile中. 你找到一些有用的配置片段或者你想要使用非常有用的. 例子:

```
Vagrant.configure("1") do |config|
  # v1 configs...
end

Vagrant.configure("2") do |config|
  # v2 configs...
end
```

```
什么是`Vagrant::Config.run`?你可以在Vagrantfiles中看到. 这是的确是以前Vagrant1.0.x的配置. 在Vagrant1.1以上, 这个的同义词是 `Vagrant.configure("1")`.
```
