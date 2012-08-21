---
author: hewig
title: >
  MeeGo开发Tips（0）非Intel图形芯片使用Xephyr模拟器
excerpt:
layout: post
category:
  - MeeGo
tags:
  - meego
  - meego sdk
post_format: [ ]
---
### 根据MeeGo Wiki上的[MeeGo SDK with Xephyr][1]教程，执行：

$ lspci | grep VGA

如果不是intel的图形芯片（比如杯具的nvidia，不知为何ati的反倒是可以使用），就得see the[ other SDK options][2]（MeeGo SDK本身可以使用，如libmeegotouch，不能使用的是基于Xephyr的emulator，会黑屏）。

怎样在非intel图形芯片上使用Xephyr呢？intel的合作伙伴nokia论坛出了个[教程][3]，详细的一笔。

#### 简单来说就是安装并运行外部的Xserver-Xephyr（nested x server），DISPLAY设置为:2，然后在MeeGo SDK中启动emulator时，设置DISPLAY为:2。

$ sudo apt-get install xserver-xephyr

//根据教程，在运行xhost命令之后执行：

$Xephyr :2 -host-cursor -screen 1024x768x16 -dpi 192 -ac  &

$export DISPLAY=:2

//chroot到meego sdk路径后

$startmeego &

不过每次都这么敲命令会很麻烦，可以写入一个文件里，然source执行![][4]

效果如下，不过运行的很慢。。![][5]

最后普及一下：什么是Xephyr呢？参考[这里][6]

Xephyr is a kdrive based X Server which targets a window on a host X Server as its framebuffer. Unlike Xnest it supports modern X extensions ( even if host server doesn’t ) such as Composite, Damage, randr etc (no GLX support now). It uses SHM Images and shadow framebuffer updates to provide good performance. It also has a visual debugging mode for observing screen updates.

Xephyr 是一个 Xnest 的替代产品，因为 Xnest 不提供现代 X server 的一些高级特性，比如图形加速的支持。简而言之，Xephyr 是一个 X server，但是它执行在一个存在的 X server 里面，这个可以用来做很多事情，比如需要通过 XDMCP 连接到另外一台主机，那么不需要另外打开一个新的 X server；又比如正在写一个 window manager，那么在一个 X server 里面打开的 X server 里面调试，将会比直接在现有的 X server 里面替换现有的 window manager 方便很多。对于热衷于更换自己的 window manager 的狂热爱好者，Xephyr 提供了绝佳的试验环境。 [![][8]  
][8]  

 [1]: http://wiki.meego.com/MeeGo_SDK_with_Xephyr
 [2]: http://wiki.meego.com/MeeGo_SDK_Development_Options
 [3]: http://wiki.forum.nokia.com/index.php/Qt_MeeGo_handset_SDK_how_to_install_and_use_on_Linux_Ubuntu_10.04_LTS
 [4]: https://lh3.googleusercontent.com/ziHvfgiAYt02R81VDelMlKUTBS4ysRfBsxbYmd1Bp0t1pKPf3uOHWT_WV5jq3xIvdvc3VYIXJNZxVUfLuEBGwdPPip2Keh3L8F0aDITcEWp-DNKgxg
 [5]: https://lh6.googleusercontent.com/j-Dap3Zf8d56M4I-hTwgM3GZEVhSbpRuonxdMgWVJ7zm90aWQGxD_d0w7GhqaNUC38af1YFKaXUTrKU-xGfyghoAbTTezpD0buPcGZqBNAXRPqFFGA
 [6]: http://www.freedesktop.org/wiki/Software/Xephyr
 []: javascript: