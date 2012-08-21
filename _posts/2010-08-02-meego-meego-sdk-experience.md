---
comments: true
date: 2010-08-02 06:48:00
layout: post
slug: meego-meego-sdk-experience
title: Meego & Meego SDK体验
wordpress_id: 25
categories:
- Linux
- MeeGo
tags:
- meego
---

#### MeeGo & MeeGo SDK 体验教程


**0.MeeGo简介**

MeeGo项目结合英特尔的Moblin和诺基亚的Maemo, 为下一代计算设备打造了一个基于Linux的开源软件平台。MeeGo软件平台为开发人员的应用程序提供了最大范围的设备选择，包括上网本和入门级桌面设备，便携式计算和通讯设备，车载信息娱乐设备，联网电视，媒体电话等等－均使用共同的开发框架Qt。MeeGo将帮助消费者从不同的设备中获得创新的应用程序体验。MeeGo项目由Linux基金会管理。MeeGo为Linux基金会商标。（来源[MeegoZone中文站](http://meegozone.csdn.net/meego.aspx)）

MeeGo的[MeeGo架构设计](http://meego.com/developers/meego-architecture)，可以去看看，如下图：[![clip_image002](http://kernelpanic.im/blog/wp-content/uploads/2010/08/clip_image002_thumb.gif)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/clip_image002.gif)

MeeGo很大一个特点是开源，多平台，并交由Linux基金会管理；产品种类可包括笔记型电脑，智慧型手机，小笔电，平板电脑，互联网电视和车载资讯娱乐系统等。为此，诺基亚还分别调整了Symbian和MeeGo的策略与定位，原有的Symbian平台将继续致力于智能手机的大众化（应该是现有的主流S60/S40，之后的Symbian^3/4好像不大现实，首款采用[Symbian^3系统--N8](http://news.mydrivers.com/1/170/170746.htm)报价469欧）MeeGo则主要定位于高端市场。诺基亚收购Qt，将跨平台的开发特性带给了Desktop、Symbian、MeeGo，其中Meego的编程接口,除了QT 4.7 和WRT还有MeeGo多点触摸界面框架(MeeGo Touch UI Framework 简称MTF)。这种开放的姿态很受开发者欢迎，至于消费用户可能就不会这么看了。MeeGo系统目前也未发布什么像样的产品，只是放出了MeeGo-handset/notebook的img镜像，以及Meego SDK。根据[InfoQ上一篇移动开发调查报告](http://www.infoq.com/cn/news/2010/07/Mobile-Survey)，与Iphone/Android高关注相比，MeeGo就像一个仓促上阵的参赛者（两个发行版的整合好像费一些时间，毕竟一个是基于稳定代名词的Debian，另一个则基于“不稳定”代名词的Fedora），在调查报告中都没提到。造成诺基亚的危机主要是在市场占有率常年第一时的不思进取，这和微软最初对待互联网、几年不更新的IE6很像；不过这一次玩的有点大，Symbian系统的用户体验一直没有什么进步，Symbian的开发效率更是让人诟病。。。不过话说回来诺基亚向来是后发先制，UCD大社区有篇文章[相信诺基亚](http://ucdchina.com/snap/7488)，就提到了这个观点，就让时间去证明吧。

**1. Meego安装体验**

0> MeeGo 1.0运行目前是有一些限制的：

a) 处理器：英特尔Atom或32位的Intel Core 2处理器（支持SSSE3）

[![ceI5TrAm0YdZY](http://kernelpanic.im/blog/wp-content/uploads/2010/08/cei5tram0ydzy_thumb.jpg)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/cei5tram0ydzy.jpg)

b) 显卡：一个兼容的Intel图形芯片组。不支持GMA-500/Nvidia/ATI的芯片组。
备注：MeeGo将不能在非SSSE3处理器上运行，更多的硬件配置将在系统的后续更新中获得支持。

c) 不支持NTFS文件系统（不过这不是问题，因为它是Linux，自己动手）

d) 官方承诺可以运行MeeGo操作系统的几款上网本分别为：ASUS EeePC 901/1000H/1005HA/1008HA/1005PE、Eeetop ET1602、DELL mini10v、Inspiron Mini 1012、Acer Aspire One D250、AO532-21S、Revo GN40、Aspire 5740-6025
lenovo S10、MSI U130、AE1900、[HP](http://www.hbea3w.com/Search.asp?KeyWord=HP) mini 210-1044、Toshiba NB302，支持触控操作。

1> 在[MeeGo官网](http://meego.com/downloads)下载最新镜像，img格式，handset对应手机，notebook对应笔记本。。

2> 如果想在虚拟机上安装Meego，会比较失望，主流的VMWare和VirtualBox均不能显示启动Meego的图形界面，因为不是Intel图形芯片组。不过Meego SDK中的模拟器还是可以启动的，然后可以体验一下meego。在Windows上建议使用VirtualBox，相比于VMWare，virtualbox快多了；在Linux下其实就没有必要用虚拟机了，SDK本身就可以用，如果要安装的话，qemu或者virtualbox都是不错的选择，可以参考[MeeGo Wiki](http://wiki.meego.com/MeeGo_1.0_Netbook_VirtualBox)，下图是Qemu的截图

[![meego-ivi-qemu-011](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meegoiviqemu011_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meegoiviqemu011.png)

3> 如果在虚拟机上选择“Boot Meego”：会停留在黑屏界面，下面步骤可解决～

[![boot_menu](http://kernelpanic.im/blog/wp-content/uploads/2010/08/boot_menu_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/boot_menu.png)

a) Press ESC when the boot begins to get into GRUB boot menu.

b) Press TAB to edit boot line.

c) Remove quiet from boot line and append 3 to start with a shell and then boot.

d) After boot is complete, press ALT-F1 to get into console and login using your user account. 这两步是关键，卡在黑屏的时Alt+F1切换到控制台登录模式，可以使用root登录,密码meego；进入后执行init 3，要不然老是会跳到无法启动的图形界面去

e) Type sudo startx to start X11 with TWM :) TWM还是能够启动的，不过相当“简陋”，下图

[![Meego-x11-twm-virtualbox](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meegox11twmvirtualbox_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meegox11twmvirtualbox.png)

4> 最好不要尝试“Installtion Only”，我试过好几回，安装完成后的第二次重启会一直卡在背景处，连文本模式都进不去，原因不明，如果你找到了解决方法，请告诉我～

5> 如果你有满足MeeGo目前限制的笔记本，最好的体验方法就是刻盘启动Meego，或者是将MeeGo安装到U盘或者移动硬盘上（一般的Linux都是支持的，一个小工具Unetbin就能搞定），这样能够体验到完整的Meego环境。不过由于不是触屏设备，普通笔记本上的MeeGo给人的第一印象只是一个界面可爱华丽的Linux普通发行版而已，同样采用了yum进行包管理，集成了常见的一些软件。不上图了，图效果同最后模拟器。。

6>在线安装软件可以yum search [firefox]，yum install [firefox]，rpm –ivh [firefox-noarch.rpm]

**2. Meeg
o SDK体验**

0> MeeGo SDK由以下部分构成：

a) 一个MeeGo chroot环境，这包含了一个基于[Xephyr](http://www.freedesktop.org/wiki/Software/Xephyr) 的MeeGo应用程序模拟器（仅支持Linux），一些在Xephyr里启动/停止MeeGo桌面的脚本，以及可以远程配置和部署MeeGo设备的Qt Creator。

b) 一个启动MeeGo chroot环境，并运行模拟器和Qt Creator的_meego-sdk-chroot_脚本

1> 下载MeeGo SDK大概630M，不过我觉得SDK和Gentoo stage3的tar包很像，不同的是它包含了Qt完整开发toolchain、模拟器的chroot环境。

2> 按照目前的很常见的开发模式，大家都习惯于在Windows/Linux上开发-->模拟器测试-->真机测试。不过现在由于现在的一些限制，在linux下开发是最简单的。按照[在Linux 上使用MeeGo SDK](http://wiki.meego.com/%E5%9C%A8_Linux_%E4%B8%8A%E4%BD%BF%E7%94%A8_MeeGo_SDK)上的步骤，有时会遇到模拟器后启动白屏或者黑屏的问题，这里有一个小bug，meego sdk的mailist提供了一个[解决方法](http://lists.meego.com/pipermail/meego-dev/2010-June/003088.html)。

3> 由于每次启动sdk需要配置xhost,以及执行chroot命令，还有可能存在上面的一个小bug，我建立了一个脚本start_meego，然后使用source命令执行，这样可以省事不少。

#start_meego

#[ ]内替换为你当前路径

export DISPLAY=:0

export DBUS_SESSION_BUS_ADDRESS=""

xhost && xhost +SI:localuser:[root]

[./meego-sdk-chroot] [./meego-sdk-0524]

[![source_meego](http://kernelpanic.im/blog/wp-content/uploads/2010/08/source_meego_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/source_meego.png)

4> 在Windows下要想体验meego sdk,目前好像只有使用虚拟机安装Linux这一种方法，比如Ubuntu之类的。而我这次安装的是gentoo使用的是install-x86-minimal镜像，光emerge kde-meta就花了三天时间，期间还安装了X，和Virtualbox Guest Addtions，才让它工作正常。所以最好还是安装集成版，或者安装轻量级的X Window。下面是MeeGo模拟器的一些截图，和真机跑效果是差不多的～

[![meego_emu](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_emu_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_emu.png)

欢迎界面

[![meego_develop](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_develop_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_develop.png)

应用软件

[![meego_multi_task](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_multi_task_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_multi_task.png)

多桌面切换

[![meego_device](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_device_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2010/08/meego_device1.png)

设备界面，由于是模拟器，电池，无线不可用

5> 剩下的就是打开Qt Creator/Desinger，创建应用了。体验Over~
