---
title: 卸载多余内核
categories:
  - Kernel
tags:
  - Remove
  - Linux
date: 2024-11-30 08:20:17
---

前言:Linux每次更新内核，旧内核不会自动删除，占用空间。

注意:卸载内核前，确保保留的内核可以启动，以免悲剧发生，本教程后续会进行完善。


## 查看当前的内核

```sh
uname -a
``` 

## Debian&Ubuntu

查看当前系统中所有内核
```sh
dpkg --get-selections |grep linux
``` 

以Ubuntu为例:当前系统中所有内核(精简了部分显示信息)
```sh
linux-headers-5.19.0-16                install
linux-headers-5.19.0-16-generic        install
linux-image-5.19.0-16-generic          install
linux-modules-5.19.0-16-generic        install
```

清理多余的系统内核(复制需要卸载的内核名称，如下面示例)
```sh
sudo apt purge linux-headers-5.19.0-16 linux-headers-5.19.0-16-generic linux-image-5.19.0-16-generic linux-modules-5.19.0-16-generic 
```

删除内核后需要更新grup移除失效的启动项
```sh
sudo update-grub　#根据情况选择grub/grub2
```

## Fedora
>自动卸载旧内核

卸载命令

```sh
sudo dnf remove --oldinstallonly 
```

清理多余依赖
```sh
sudo dnf autoremove
```

## Arch
>自动卸载旧内核
```sh
sudo pacman -R linux
```

删除内核后需要更新grup移除失效的启动项
```sh
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
