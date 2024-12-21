---
title: 使用Wine运行windows软件
categories:
  - Linux
tags:
  - Wine
  - Windows
  - Install
date: 2024-12-21 22:38:53
updated: 2024-12-21 22:38:53
---

# Wine的使用入门

## 在Linux上借助Wine运行Windows应用和游戏

Linux系统不能直接运行Windows的exe程序，但是如果遇到某些应用和游戏没有Linux原生版本，只有Windows的exe，而且还需要在Linux系统运行这些应用和游戏的情况，这时候可以借助Wine或Proton来运行这些程序。

### 使用Wine运行器运行Windows应用

原版Wine只能用命令操作，比较繁琐，对小白不友好。为此，gfdgd xi制作了“Wine 运行器”，将Wine命令GUI化并附带安装Wine的功能，使运行Wine的操作更加简单。

1. 首先需要下载“Wine 运行器”，可以通过星火应用商店下载

![](/img/posts/wine-run/wine-runner-1.webp)

2. 下载好后安装，安装完成后打开软件主界面

![](/img/posts/wine-run/wine-runner-2.webp)

3. 点击运行器左上角“程序”-“安装更多 Wine”，然后在弹出的窗口中的右侧框选择需要的Wine版本（这里以deepin-wine8-stable为例）

![](/img/posts/wine-run/wine-runner-3.webp)

![](/img/posts/wine-run/wine-runner-4.webp)

4. 等进度跑完，选择安装的版本出现在左侧框时就表示安装成功，此时关闭窗口，回到主界面，会发现“请选择Wine版本”下面的框显示了所安装的Wine版本

![](/img/posts/wine-run/wine-runner-5.webp)

5. 在中间的“请选择要执行的程序”框内选择要运行的应用路径（这里以千千静听为例）

![](/img/posts/wine-run/wine-runner-6.webp)

6. 最上面的“请选择容器路径”一般不用改，默认即可（除非需要不同的容器环境测试或者需要打包Wine应用）；然后点击右下角“运行程序”

7. 运行效果如图所示

![](/img/posts/wine-run/wine-runner-7.webp)

8. （可选）如果想方便启动程序的话，可以通过建立桌面图标或者启动器图标进行启动该Wine程序

![](/img/posts/wine-run/wine-runner-8.webp)

### 使用Wine游戏助手运行国内大厂游戏

（这里以原神为例，其他类似网游也可使用类似方法，但不保证所有网游都能运行成功）

1. 安装游戏本体。理论可以通过An anime game launcher下载 **（未经测试！）**，然后将它放在NTFS分区。

2. 在wine运行器中安装任意版本GE proton wine，在wine运行器主页“选择wine版本”栏的下拉菜单中会有具体路径。
![1-2-1.png](https://storage.deepin.org/thread/202308301730531280_%E6%88%AA%E5%9B%BE_deepin-wine-runner_20230830173002.png)

回到wine游戏助手，如图操作，填入路径即可。
![1-2-2.png](https://storage.deepin.org/thread/202308301733409725_%E6%88%AA%E5%9B%BE_lutris_20230830173217.png)
![1-2-3.png](https://storage.deepin.org/thread/202308301734095897_%E6%88%AA%E5%9B%BE_lutris_20230830173306.png)

3. 下载wine游戏助手，然后打开它，首先点左上角+号，然后弹出的框中选‘‘在winegame网站搜索游戏’’（截图中我还省略了一步）然后在弹出的搜索框搜启动自定义游戏，点击搜索结果接着选最顶上那个“带完整DXDLL的64位wine7.1”，点安装。
![1-3-1.png](https://storage.deepin.org/thread/20230830172228638_202301121639407037_%E6%88%AA%E5%9B%BE_lutris_20230112163536.png)

4. 然后选择“YuanShen.exe”所在路径，点继续，等它操作完成就可以啦
![1-3-2.png](https://storage.deepin.org/thread/202308301723191087_202301121641514647_%E6%88%AA%E5%9B%BE_lutris_20230112164141.png)

注意：Wine本质只是一个兼容层，并不能保证运行全部的Windows应用；如果遇到无法运行或者运行报错的情况，可以尝试下安装对应组件、启用或禁用功能、更换Wine版本尝试下。如果这样试过后依然无法运行，建议Windows虚拟机或Win+Linux双系统
