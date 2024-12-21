---
title: Linux 和 Windows 时间不同步
categories:
  - Linux
tags:
  - Time
  - Windows
reprint: true
author: xuqi
avatar: 'https://avatar.cdn.deepin.com/public/avatar/2022/11/24/15-23-58-e3363b76.png'
date: 2024-11-30 08:12:43
updated: 2024-11-30 08:12:43
---

##  一、 Windows的时间和时区

Windows操作系统直接把CMOS时间认定为当前显示时间，不根据时区转换。这样每调整一次系统时区，系统会根据调整的时区来计算当前时间，确定后，也就同时修改了CMOS内的时间（即每调整一次时区，设置保存后，CMOS时间也将被操作系统改变一次，注意不同操作系统调整时间后，也会同时改变CMOS时间，这一点是共通的）。

## 二、 Linux的时间和时区

Linux和苹果操作系统以当前主板CMOS内时间做为格林威治标准时间，再根据系统设置的时区来最终确定当前系统时间（如时区设置为GMT+08:00北京时间时以及当前CMOS时间为03:00，那么系统会将两个时间相加得出显示在桌面的当前系统时间为11:00）

## 三、 问题解决

解决的办法有两个

让Windows使用Linux的时间管理方式，就是启用UTC（世界协调时）

让Linux按照Windows的方式管理时间，就是让Linux禁用UTC（世界协调时）

个人**推荐**第二种，因为通常Windows是主系统，不推荐对Windows进行修改：

1. 在Windows下启用UTC

打开运行窗口（快捷键Win+R），然后输入regedit启动注册表编辑器，并找到`HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Control/TimeZoneInformation/`位置（可以直接粘贴进注册表编辑器地址栏），然后添加一项类型为`REG_DWORD`的键值，命名为`RealTimeIsUniversal`，值为 `1` 。重启后时间即回复正常

2. 在Linux下关闭UTC

调出终端，输入：
```sh
sudo gedit /etc/default/rcS
```
找到`UTC=yes`这一行，改成`UTC=no`然后Ctrl+S保存即可，时间修改立即生效。这样就可以解决Windows与Linux双系统时间同步问题了。

3. Linux 时钟设置 —— timedatectl 

在Linux下打开终端，依次输入以下命令：
```sh
timedatectl set-local-rtc 1
timedatectl
```
