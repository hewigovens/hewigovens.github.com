---
layout: post
title: "Port gevent to iOS"
description: ""
category: 
tags:
- python
- gevent
- iOS
- port
---
{% include JB/setup %}

什么是[gevent](http://www.gevent.org/)：
		
>
gevent is a coroutine-based Python networking library that uses greenlet to provide a high-level synchronous API on top of the libevent event loop.
>
		
GoAgent local从2.x之后，用gevent重写了，一般来说gevent还是比较适合写server程序，但是GoAgent比较特殊，proxy本来也算server。用gevent好处有很多，比如改善并发的效率，减少内存使用，写起来也很顺手；坏处是gevent并非属于标准库，而且含有C的extension，所以每个平台都需要至少编译一遍，其关键依赖--greenlet的切换基本上通过寄存器保存当前执行栈的情况，这个也是和硬件、平台密切相关的。

总结起来其实还蛮简单的：  


* 在iOS设备上搭建编译环境并安装python，具体可以参考wiki:[Develop Jailbreak Apps](https://github.com/hewigovens/hewigovens.github.com/wiki/Develop-Jailbreak-Apps)  

* `git clone https://github.com/hewigovens/gevent-for-ios`
* - ----这次移植的版本是1.0b4，最新的应该是rc1，看了下[Changelog](https://github.com/SiteSupport/gevent/blob/master/changelog.rst) 改动还不少，不过还好greenlet满足要求，所以问题应该不大

* `git clone git://github.com/snaury/greenlet` 然后 `git checkout wip-iphone`
* - ----这个是Snaury移植的greenlet 0.3.4，关键~  
* 分别python setup build

当然在Mac上cross compile也是可以的~，稍后会打包成deb或者egg
