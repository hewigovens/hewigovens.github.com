---
author: hewig
title: 也谈恶意竞争
excerpt:
layout: post
category:
  - Life
  - Tricks
tags:
  - ssh
post_format: [ ]
---
今天早上本来想通过网银充手机话费，结果江苏移动网上营业厅的验证码老是刷不出来，结果导致无法登录。

[![direct][2]][2]

firefox直接访问

[![direct_ie][3]][3]

IE直接访问

我第一时间的想法是用代理试一下，看看是不是有问题，于是挂上ssh~

[![proxy][4]][4]

firefox代理访问，一切正常，但是由于不思进取的各大网银系统，加上IE Tab还不能把安全插件加进去，最终无法也完成支付，无奈之下，经过一番设置，把IE挂上了ssh的代理

[![proxy_ie][5]][5]

> IE代理访问也正常了

IE 使用ssh代理，要注意一点：由于ssh tunnel转发是socks的方式，所以在IE设置时应该在“advanced”最后一行socks里填写地址和端口，并且清空http/https/ftp栏的设置，如下图：[![ie_proxy][6]][6]

设置好了之后，可以考虑安装proxypal，ie下的代理开关小工具，功能弱了点，但是还能用用，开心了可以自己拿bat或者py操作注册表，就是几个键值的问题，这主要是受对面phus的影响，工具使得很溜。

后来我无意中看到一篇文章–[江苏电信封杀江苏移动网上营业厅?通信业3Q大战][6]，时间也是12月份的，然后我查了下ip，果然是电信的IP[![no_proxy_ip][8]][8]

这就是赤果果的恶意竞争啊，在不健全的体制下更是如此，网易科技的一篇[TD：最坏的自主创新][8]，道出了中国特色的创新，有人会说之前怎么不说，很明显，之前被集体禁声，反对的声音根本发不出来，还有一个搞笑的[中国高铁偏爱英文操作手册？][9]，戳穿了所谓的中国高铁自主知识产权。。 [![][11]  
][11]  

 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/direct.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/direct_ie.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/proxy.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/proxy_ie.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/ie_proxy.png
 [6]: http://www.shanzhaiji.cn/opinion/20101212/21898.html
 []: http://kernelpanic.im/blog/wp-content/uploads/2010/12/no_proxy_ip.png
 [8]: http://tech.163.com/10/1228/08/6OVRHA0500094IR6.html
 [9]: http://www.ftchinese.com/story/001036182
 []: javascript: