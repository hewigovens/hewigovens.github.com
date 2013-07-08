---
comments: true
date: 2011-01-09 21:54:11
layout: post
slug: ssh-over-usb
title: SSH over USB
wordpress_id: 178
categories:
- Linux
- Tricks
tags:
- ipod touch
- ssh
---

某天在wiki上闲逛，发现一个[SSH_Over_USB](http://www.iphonedevwiki.net/index.php/SSH_Over_USB)的entry，可以让SSH通过USB数据线来连接iOS，上面说的是在Mac OS下，当然在linux和Windows下也是可以的。原理是什么呢，是在Local运行一个usb多路复用（multiplexor）的daemon，然后运行client程序通过它建立本地<—>远程端口转发，最后就可以使用ssh进行基于usb tunnel的连接了。这个有什么用呢？对于jb/unlock肯定是有帮助的，还可以开发cydia上的app，折腾（可以装web server，或者在上面写python，java），甚至crack wifi密码都可以（现在暂时还不行）。

 

1.安装usbmuxd，可以看到在Ubuntu源里已经包含了，这里八卦一下，Mac App Store发布了，里面包含了1000多个应用，你可以下载/购买，更新，sounds familiar，linux folks？（see ：[Apple, Linux welcomes you to 1998!](http://www.networkworld.com/community/node/70405)）

 

#sudo apt-get install usbmuxd

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/usbmxd_zpsaf58be48.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/usbmxd_zpsaf58be48.png" width=100% border="0" alt=" photo usbmxd_zpsaf58be48.png"/></a>

 

2.usbmuxd的[作者](http://marcansoft.com/blog/iphonelinux/usbmuxd/)提供了一个简易的python-client，运行它，可以看到将本地的2222端口转发到了远程的22端口（即被将被连接的iDevice）

 

#./tcprelay.py –t 22:2222

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/daemon_listen_zps0eebb8bd.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/daemon_listen_zps0eebb8bd.png" width=100% border="0" alt=" photo daemon_listen_zps0eebb8bd.png"/></a>

 

3.建立ssh连接，#ssh [root@127.0.0.1](mailto:root@127.0.0.1) –p 2222

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/ssh_ipod_zps764e5609.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/ssh_ipod_zps764e5609.png" width=100% border="0" alt=" photo ssh_ipod_zps764e5609.png"/></a>

 

python-client的回显，连接建立了

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/daemon_accept_zps6d0518cf.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/daemon_accept_zps6d0518cf.png" width=100% border="0" alt=" photo daemon_accept_zps6d0518cf.png"/></a>

 

 

在Windows下就很简单了，最新版本的ifunbox，提供了USB Tunnel的功能，点击下USB Tunneling，如图

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/Untitled4_zps8a177e8e.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/Untitled4_zps8a177e8e.png" width=100% border="0" alt=" photo Untitled4_zps8a177e8e.png"/></a>

 

将本地的22端口转发到远程的22端口

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/Untitled3_zpsacf466be.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/Untitled3_zpsacf466be.png" width=100% border="0" alt=" photo Untitled3_zpsacf466be.png"/></a>
 

ssh连接之，现在可以干很多事情了~

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/01/Untitled5_zpsb85f9a49.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/01/Untitled5_zpsb85f9a49.png" width=100% border="0" alt=" photo Untitled5_zpsb85f9a49.png"/></a>
