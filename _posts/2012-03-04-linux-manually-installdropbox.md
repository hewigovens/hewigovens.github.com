---
author: hewig
title: Linux下安装Dropbox
excerpt:
layout: post
category:
  - Linux
  - Tricks
tags:
  - Dropbox
post_format: [ ]
---
上周想在Ubuntu底下接着写一个未完成的shell脚本，直接扔进Dropbox里了。回来的时候发现笔记本上的Ubuntu并没有安装Dropbox，话说以前我一直用Ubuntu One的，从Dropbox官网下载了对应的deb包，安装完运行的时候总是提示无法连接到服务器，设置http代理、ssh代理，改host均无效（也有可能是我姿势不对）。后来在Fanxi的提醒下找到了原因。

[Dropbox for linux][1]其实只是nautilus-dropbox，并不完整，nautilus-dropbox运行之后需要从Dropbox的网站下载缺少的binary文件，而始终无法连接不到服务器的提示其实是指无法下载这个依赖文件(dropbox-lnx.x86.xxx.tar.gz). wireshark抓包截图说明了这一点，链接直接被RST了，原因嘛。。

[![Wireshark抓包图][3]][3]

知道这一点就好办了，根据wireshark抓包的那个Get请求手动从Dropbox网站下载这个dropbox-lnx.x86.xxx.tar.gz，然后解压之，注意它是个隐藏文件夹.dropbox-dist

[![][4]][4]

然后mv到~目录下，dropbox start -i 应该就可以运行了.

[![][5]][5]

已经在同步了~

[![][6]][6]

[![][7]  
][7]  

 [1]: https://www2.dropbox.com/install?os=lnx
 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/Selection_001.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/Selection_002.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/Selection_003.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/Selection_004.png
 []: javascript: