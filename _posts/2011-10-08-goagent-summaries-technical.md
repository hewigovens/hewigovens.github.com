---
comments: true
date: 2011-10-08 23:30:07
layout: post
slug: goagent-summaries-technical
title: GoAgent小结--技术篇
wordpress_id: 370
categories:
- iOS
- Python
tags:
- goagent
- iOS
- python
---

**2011/12/8 Update**
具体实现细节，请访问goagent-dev之[goagent做了哪些改进？](https://groups.google.com/forum/#!topic/goagent-dev/QLrWFUkdT_0)


GoAgent 一直号称简单快速，不是没有道理的。proxy.py不到800行的代码实现了：跨平台运行、多appid负载均衡、RangeFetch、支持NTLM、支持内网代理、支持ipv6、支持php fetch等诸多feature，其考虑到的一个重要原则是依赖尽可能小，这体现在了：


> 
0.代码即程序，Windows下绿色运行，连GAE的sdk都不用装，这得益于先进的打包技术。
1.实现基本上都是标准库，openssl库也很常见，移植容易。
2.fetch.php对服务器端的要求较低。需要preg/zlib/curl模块支持，前两个属于标准模块，curl也是常见模块。
3.合理的默认值，只需要配置appid就可以用了。
4.不支持gfwlist



GoAgent 另一个原则就是追求速度，不断在优化，看看[ChangeLog](https://code.google.com/p/goagent/wiki/ChangeLog)就知道了：


> 
0.压缩传输，不支持强加密，因为连GMail都被天朝黑客入侵过，保证local到AppEngine的绝对完全并没有太多的意义。。
1.再如之前整合了gevent或者线程池，为了速度后来又拿掉了；
2.为了加快启动速度，将读取proxy.ini 放入了全局变量中，代码因此丑陋了；
3.修正了socket关闭速度慢的问题；
4.多次重新打包python解释器(proxy.exe)；
5.简单到极致的GUI，在启动时完成大部分初始化设置并减少if的使用；
6.为了优化php fetch的规则匹配，干脆将其和GAE的监听端口分开；



GoAgent的优势在于在客户端做了大量工作，由本身维护session的状态， 因为GoAgent 既是Client又是Server，本地相当于一个http server（采用了BaseHTTPServer），同时又是Client端，与部署在AppEngine的fetch.py进行通信。所以当我得知有些代理软件使用mysql来维护代理服务器的session状态时，觉得有点惊讶，明显不合理了嘛。另外基于GAE的代理最快的就是直连北京google了，因为Google的很多服务都是云服务，所以一个IP能够提供多种服务，其中就包括AppEngine，因此访问google自家的服务速度很快，而GoAgent 从一开始就是这么做的。

关于Porting的问题，比如支持iOS，我认为移植平台本身更为容易，所以才有很多人打Android应用的主意，比如最开始的Alien Dalvik，号称让MeeGo支持Andorid 25W应用的[ACL for MeeGo](http://tech.weiphone.com/2011-09-23/translator_fail_241650.shtml)，裁剪VirtualBox的[BlueStack](http://www.bluestack.com)，一直不温不火的[Mobile Virtualization](http://www.google.com/search?q=mobile+virtualization)，尽管这些目前看来还不太实用，比如BlueStack，我就挺好奇它如何解决ABI不同的问题，但是都是移植平台的例子~

咳，有点扯远了，所以支持iOS最关键的无非就是：1.交叉编译python2.6 for iOS 2.编译pyOpenSSL for iOS。其他的都是如何让设置变得简单，操作简便而已。顺带提一句，pyOpenSSL和SBSetting GoAgent toggle都是在我的ipod上编译的，越狱开发其实门槛也不高，只要搞定了toolchain就ok。

最后再八卦几句，GoAgent 最开始是托管在github上（其实现在也是），后来为了不"牵连“github，迁移到了Google Code上，在首页上用了一个空的bit.ly 链接指向了真实的地址，原因也是如此；GoAgent 的名字是因为不想再用已经泛滥的proxy。。
