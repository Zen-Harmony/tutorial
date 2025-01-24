---
title: Linux 和 Windows 时间不同步
categories:
  - Linux
tags:
  - Time
  - Windows
reprint: true
author: 萱儿
avatar: 'https://avatars.githubusercontent.com/u/195874275?s=400&u=b9a898cd79b75a991a4a7ab0625185f28ec2d39b&v=4'
date: 2024-11-30 08:12:43
updated: 2025-01-24 08:12:43
---

## 一、时间与时区管理方式

### Windows：

- 直接将CMOS时间认定为当前显示时间，不根据时区进行转换。

- 调整时区时，系统会根据新时区计算当前时间，并同时修改CMOS时间。

### Linux：

- 将CMOS时间作为格林威治标准时间（GMT）。

- 根据系统设置的时区来确定最终显示的当前系统时间。

## 二、问题解决方案

为了解决Windows和Linux在时间管理上的差异，可以采取以下两种方案之一：

1. 让Windows使用Linux的时间管理方式（启用UTC）：

在Windows中，通过修改注册表来启用UTC。

具体步骤：打开运行窗口（快捷键Win+R），然后输入regedit启动注册表编辑器，并找到`HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Control/TimeZoneInformation/`位置（可以直接粘贴进注册表编辑器地址栏），然后添加一项类型为`REG_DWORD`的键值，命名为`RealTimeIsUniversal`，值为 `1` 。

重启后，Windows将使用UTC方式管理时间。

2. 让Linux按照Windows的方式管理时间（禁用UTC）：

> 注意：linux改成`localtime`可能会受夏令时影响（仅限部分地区）

- 在Linux中，通过timedatectl命令将硬件时钟设置为本地时区。

- 使用`timedatectl set-local-rtc 1`命令将硬件时钟设置为本地时区。

- 相应地，如果需要设置为UTC，则使用`timedatectl set-local-rtc 0`命令。

通过以上方法，可以在Windows和Linux之间实现时间管理的一致性，避免时区调整带来的时间错误问题。

## 三、Linux时钟设置详细教程

1. 查看时间和时区：

- 使用`timedatectl status`查看系统当前时间和日期。

- 使用`timedatectl | grep Time`查看当前时区。

- 使用`timedatectl list-timezones`查看所有可用时区。

2. 设置硬件时钟：

- 使用`timedatectl | grep local`查看硬件时钟是否设置为本地时区。

- 使用`timedatectl set-local-rtc 1`将硬件时钟设置为本地时区。

- 使用`timedatectl set-local-rtc 0`将硬件时钟设置为UTC。

3. 设置时区：

- 使用`timedatectl set-timezone "Asia/Shanghai"`设置本地时区。

- 使用`timedatectl set-timezone UTC`将local_time设置为UTC。

4. 设置时间和日期：

- 使用`timedatectl set-time 13:58:30`设置时间。

- 使用`timedatectl set-time 20250124`设置日期。

- 使用`timedatectl set-time '13:58:40 2025-01-24'`同时设置日期和时间。

5. 同步系统及硬件时间：

- 使用`date`查看系统时间。

- 使用`hwclock --show`查看硬件时间。

- 使用`hwclock --systohc`以系统时钟为准，同步硬件时钟。

- 使用`hwclock --hctosys`以硬件时钟为准，同步系统时钟。
