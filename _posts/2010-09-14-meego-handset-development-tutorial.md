---
comments: true
date: 2010-09-14 11:52:26
layout: post
slug: meego-handset-development-tutorial
title: MeeGo-Handset开发入门小结
wordpress_id: 27
categories:
- Linux
- MeeGo
tags:
- meego
- meego sdk
---

**关于MeeGo的版本**
在MeeGo[官网](http://meego.com/downloads/releases)主要有3个：

[MeeGo Handset Day1 Developer Preview](http://meego.com/downloads/releases/1.0.80.8/meego-handset-day1-developer-preview)

[MeeGo v1.0 for In-Vehicle Infotainment (IVI)](http://meego.com/downloads/releases/1.0/meego-v1.0-in-vehicle-infotainment-ivi)

[MeeGo v1.0 for Netbooks (Google Chrome Browser)](http://meego.com/downloads/releases/1.0/meego-v1.0-netbooks-google-chrome-browser)

分别代表手机版，上网本（可能之后平板？），车载设备（GPS之类的）下载下来文件名如下

meego-handset-ia32-netbook-mtf-1.0.80.12.20100723.1.img

meego-ivi-ia32-noemgd-1.0.1-20100729.1.iso

meego-netbook-chromium-ia32-1.0-20100524.1.img

meego-netbook-ia32-1.0.80.11.20100720.1.img

这些都是安装在真机的OS镜像，稍微解释一下

handset-ia32-netbook-mtf是指在ia32（x86）上运行handset版的meego，mtf代表meego touch framework，体验得是触碰屏才行【截图】

ivi-ia32-noemgd是指使用x86芯片的车载设备，用pc也是可以引导的【截图】

netbook-chromium是指默认浏览器是chromium(chrome的开源版本)的上网本OS
这 3个版本，主要是UX层不同，其中meego core都是相同的，但是SDK也会相应不同

**关于MeeGo App开发与SDK**
MeeGo的SDK有三种[方式](http://wiki.meego.com/MeeGo_SDK_Development_Options)，这里讨论的方式均指的是[Change Root (chroot) with Xephyr](http://wiki.meego.com/MeeGo_SDK_with_Xephyr) ，这种方式是速度最快的，这种方式下的sdk其实就是一个可以chroot进去的linux系统（维护过linux肯定都知道，linux挂掉的时候可以使用livecd或别的引导一下，然后挂载原来的分区并chroot进去）下载下来文件如下：

meego-sdk-0524.tar.bz2

meego-netbook-ia32-1.0.80.12.20100727.1-sdk-pre0729.tar.bz2

meego-handset-ia32-1.0.80.9.20100706.1-sdk-pre0729.tar.bz2

meego-handset-ia32-1.0.80.9.20100706.1-sdk-pre0901.raw.tar.bz2

meego-handset-ia32-1.0.80.9.20100706.1-sdk-pre0901.raw.tar.bz2

meego-netbook-ia32-1.0.80.12.20100727.1-sdk-pre0901.raw.tar.bz2

meego-sdk-0524：意思是5月24日发布的，这是最早的sdk版本，网上还有些教程是拿这个做的，这个解压就能用，不需要挂载
剩下的几个都是pre版，7月29日/9月1日发布的（pre就是很不完善的意思,==）
解开之后个是raw文件，这个是可以挂载的镜像

现 在主要工作研究handset下的开发，毕竟和iOS/Android/RIM等竞争的是这个。开发MeeGo  App可以直接使用Qt，libmeegotouch，web runtime这几种方式（这是官方推荐的）如下图，其中web  runtime(html/css/js)也是在中间那一层。![](https://lh6.googleusercontent.com/6ZfNUKGG0iDKIxTtdXpIQtBJbjynJ7bTgL6LkUQ9pTtdHWN5l5toAavI0_mZ-CFAoq6ktxumN9HhcRIz7SJ5YZxqgOZ_splW7ttiu5X6Q3yb93hmGg)

直接使用Qt是可以的，Qt4.7新增加的[Qt Quick](http://doc.qt.nokia.com/4.7-snapshot/qml-intro.html)（提供了QML）会使得开发效率更高；还可以使用libmeegotouch(MeeGo Touch Framework核心lib），这两种有什么区别？参考[这里](http://labs.trolltech.com/blogs/2010/09/10/building-the-future-reintroducing-the-qt-quick-components/)：Alan  Alpert@niqt：MeegoTouch provides a C++ widget library. If you are  writing an application UI in C++ and want native look and feel on  MeegoTouch devices, you just use it.
web runtime就直接无视了，==

**MeeGo应用程序简介**

主要由MApplication,MApplicationPage,MApplicationWindow,MLayout,MWidgets(MButton,
MComboBox,MContainer,MDialog,MMessageBox,MInfoBanner,MLabel,MList) 类组成，位置关系就如下图右边所示，都是现代GUI框架的东西，很好理解。![](https://lh5.googleusercontent.com/uzd3Hjuk2R6warhUHQc_lk14cKk7_70Yoj6EeEHT7hiPobXWSacsLiW7v8rn5sgUr0e7rczcgybOapiJrWTV7Lo_wcDo8idstwrFDC_SiOE9LzWX9w)
实际的calculator，在xephyr里运行效果图![](https://lh5.googleusercontent.com/WVFfUde7xnwp6uO0YYRRbOiiHMKiUJ_HrDi_hTwXozjaNGy4fcI0urC0V_Kp9n2PDVUfIvy4gd0bSCcc8aAtbrVu7h1B6izudYoVSKaXk8pYoPFNGA)
![](https://lh3.googleusercontent.com/avY7xYfMvR3VeJUrF3ZM9gYlzddGO9MtBPuLnHM9x4BuRqGWf8miQY0Bkcto2ZDrdYHt_m3w_FS3ygLqfEr1vxyQUlyvDLjExpMVxlxxIp_kSZdafQ)
开发API参考：

[http://apidocs.meego.com/mtf/index.html](http://apidocs.meego.com/mtf/index.html)

[http://doc.qt.nokia.com/4.7-snapshot/index.html](http://doc.qt.nokia.com/4.7-snapshot/index.html)
**使用MeeGo Touch Framework开发App**

第一种方法：普通linux发行版安装libmeegotouch库（参考[这里](http://apidocs.meego.com/mtf/installation.html)）

0.安装linux
安装的是Ubuntu10.04 LTS,由于要使用到Qt4.7  最好使用gnome桌面的发行版（其实我很喜欢KDE,但是采用KDE的发行版在默认/usr/lib下会带有稳定版本的Qt,如4.6.2,这样到编译 libmeegotouch时容易造成链接库不正确而编译失败，可能出[这个错误](http:///#)）

1.更新系统【非必须】
#sudo apt-get upgrade

2.安装toolchain，主要是git、g++和X11的libX*-dev
#sudo apt-get install git-core build-essential libgl1-mesa-dev  libglu1-mesa-dev libxdamage-dev libX11-dev libXext-dev libXtst-dev  libXrender-dev libxcursor-dev libxfixes-dev libxft-dev libxi-dev  libxrandr-dev libdbus-1-dev

3.编译Qt4.7
[下载](http://qt.nokia.com/developer/qt-qtcreator-prerelease#download)Qt4.7 源代码版（qt-everywhere-opensource-src-4.7.0-rc1.tar.gz）或者二进制版（qt-sdk-linux- x86-opensource-2010.05-rc1.bin）,前者需要手动编译，虽然时间长但是可以控制；后者安装方便，以源代码为例：
#tar xvjf qt-everywhere-opensource-src-4.7.0-rc1.tar.gz
#cd qt-everywhere-opensource-src-4.7.0-rc1
#./configure -dbus
#make
#sudo make install

完成后设置环境变量:
export QTDIR=/usr/local/Trolltech/Qt-4.7.0
export PATH=$QTDIR/bin:$PATH
若要每次生效请修改~/.bashrc,加上上面两句export命令

3.git clone libmeegotouch相关代码
#git clone git://gitorious.org/meegotouch/libmeegotouch.git
#git clone git://gitorious.org/meegotouch/meegotouch-theme.git

4.Qt4.7编译完成后,编译安装meegotouch-theme和libmeegotouch

#cd meegotouch-theme
#qmake && sudo make install

#cd libmeegotouch
#./configure
#make && sudo make install

5.运行examples测试
#cd libmeegotouch/examples/calculator
#qmake && make
#sudo ./calculator

6.安装IDE
1.qtcreator[下载](http://qt.nokia.com/developer/qt-qtcreator-prerelease#download)： qt-creator-linux-x86-opensource-2.0.1.bin
2.也可以考虑eclipse+cdt+qt-eclipse-integration的组合
#sudo apt-get install eclispse
打开eclipse->Help->Install New  Software,添加一下cdt的update-url(注意版本，这里是galileo),http://download.eclipse.org /tools/cdt/releases/galileo
http://qt.nokia.com/developer/eclipse-integration/，下载并解压放入对应eclipse安装路径(我的是/usr/lib/eclipse)

第二种方法：直接在sdk中安装libmeegotouch-devel

sdk版目前还是pre-release版本,里面带有的qt4.7和libmeegotouch基本上不是最新版，所有会有些examples无法编译通过，SDK安装可以参考meego的[wiki或者](http://wiki.meego.com/MeeGo_SDK_with_Xephyr)是我上一篇[博客](http://blog.csdn.net/xutaozero21/archive/2010/07/31/5779591.aspx)。安装完成并成功chroot后：

#zypper install libmeegotouch-devel
##复制examples中的代码测试一下
#cd libmeegotouch/examples/calculator
#qmake && make
#./calculator
