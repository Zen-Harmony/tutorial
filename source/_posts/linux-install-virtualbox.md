---
title: Linux通过run法安装和使用VirtualBox
categories:
  - VM
tags:
  - Linux
  - Install
date: 2024-12-16 09:38:53
---

在Linux安装VirtualBox时，一般根据对应的发行版版本安装对应的deb或rpm包即可；不过有时可能会遇到通过包管理器安装失败的情况，这时候可以考虑使用run法安装。

## 下载 VirtualBox

进入VirtualBox官网：[https://www.virtualbox.org](https://www.virtualbox.org)，点击右边的“Download”；

![](/img/linux-install-virtualbox/linux-install-virtualbox-1.avif)

选择“Linux distributions”：

![](/img/linux-install-virtualbox/linux-install-virtualbox-2.avif)

选择“​All distributions”：

![](/img/linux-install-virtualbox/linux-install-virtualbox-3.avif)

复制地址框上的链接：

![](/img/linux-install-virtualbox/linux-install-virtualbox-4.avif)

然后使用wget或你自己喜欢的下载器复制链接下载，这里以wget为例：

打开终端，执行：`wget https://download.virtualbox.org/virtualbox/7.1.4/VirtualBox-7.1.4-165100-Linux_amd64.run`
（这个地址会随VirtualBox的版本号更新而变化，如需最新版请根据官网版本更改地址）

![](/img/linux-install-virtualbox/linux-install-virtualbox-5.avif)

## 安装 VirtualBox

下载好后，在wget下载的run文件所在目录右键打开终端，执行：`sudo bash VirtualBox-7.1.4-165100-Linux_amd64.run`（下载的run文件名称版本号如果下载了更新或更旧的，会与此处有所不同，请以实际下载的run文件名称版本号为准）
然后输入当前用户密码后回车，开始安装，如果出现“VirtualBox has been installed successfully”就表示安装成功：

![](/img/linux-install-virtualbox/linux-install-virtualbox-6.avif)

![](/img/linux-install-virtualbox/linux-install-virtualbox-7.avif)

> 注：debian 12可能会出现无法启动VirtualBox的情况，如遇此情况，执行：`sudo apt install linux-headers-amd64 linux-headers-6.1.0-28-amd64 libxcb-cursor0`
然后重启系统即可

## 使用 VirtualBox

打开安装好的VirtualBox，会发现一条“不能枚举USB设备”的消息：

![](/img/linux-install-virtualbox/linux-install-virtualbox-8.avif)

此时需要创建usbfs组并将当前用户手动加入到vboxusers组和usbfs组。在主机系统打开终端，执行：`sudo groupadd usbfs && sudo adduser $USER vboxusers && sudo adduser $USER usbfs`

![](/img/linux-install-virtualbox/linux-install-virtualbox-9.avif)

然后注销重进系统即可生效。

除此之外，新安装好的VirtualBox还会有些许功能不全，此时还需要下载扩展包：
打开：[https://download.virtualbox.org/virtualbox](https://download.virtualbox.org/virtualbox)，然后先找到对应的版本号目录（我这里是7.1.4）：

![](/img/linux-install-virtualbox/linux-install-virtualbox-10.avif)

再选择vbox-extpack后缀的文件，选上面的，等它下载完：

下载好后双击这个文件（如果双击无效），然后选择“安装”，同意协议，输入当前用户密码后即可安装：

![](/img/linux-install-virtualbox/linux-install-virtualbox-11.avif)

然后就可以配置和安装虚拟机系统了。安装好虚拟机系统后，需要安装增强功能以获得最佳体验。在虚拟机窗口上面的菜单中选择设备-安装增强功能，然后按照以下方法安装即可：

· Windows系统虚拟机直接双击识别成CD驱动器的VirtualBox Guest Additions，按照提示安装；
> 如果双击VirtualBox Guest Additions的CD驱动器没有弹出安装界面窗口，而是直接进入该驱动器内部，则执行里面的“VBoxWindowsAdditions-amd64.exe”（64位Windows安装）或“VBoxWindowsAdditions-x86.exe”（32位Windows安装）

· Linux系统虚拟机在VBox_GAs_x.x.x（这里的x.x.x是版本号，与VirtualBox的版本号是一致的，如VBox_GAs_7.1.14）光驱目录右键打开终端，执行：`sudo ./VBoxLinuxAdditions.run`，输入用户密码，等待安装过程完成即可。

## 卸载 VirtualBox

如果不想使用VirtualBox了，想要卸载，怎么办？

打开终端，执行：`sudo bash /opt/VirtualBox/uninstall.sh`

输入用户密码执行，等待卸载完成即可。

![](/img/linux-install-virtualbox/linux-install-virtualbox-12.avif)

如果出现如上图提示，就表示卸载成功了。
