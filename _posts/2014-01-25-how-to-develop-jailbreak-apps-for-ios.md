---
layout: post
title: "浅谈iOS越狱App开发"
description: ""
category: 
tags: ['iOS','jailbreak']
---
{% include JB/setup %}

这是一篇科普性质的文章, 内容主要包括:

* 基本背景知识
* 开发环境
* Root权限
* launchd
* bypass iPhone_NA/sandbox/codesign
* SSH Tips
* Cydia Hosting

如果你对这些Topic已经足够了解, 剩下的也不用看了:)

我最早接触越狱大概是在iPhoneOS(4.0之后才改名成iOS)3.1.3时代, 印象比较深的是[@comex](https://twitter.com/comex)的[Spirit](https://github.com/comex/spirit),经典的一键完美越狱; geohot还很活跃, 一己之力搞出[Limera1n](http://theiphonewiki.com/wiki/Limera1n); 中文社区则有著名的[GFWInterpreter](https://code.google.com/p/gfwinterceptor/)...

咳咳, 不怀旧了, 开面是正文:

iOS和OS X一脉相承, kernel都来至[Darwin OS](https://en.wikipedia.org/wiki/Darwin_(operating_system)). iOS6的kernel是Darwin Kernel 13.0.0, iOS7是Darwin Kernel 14.0.0(来源:[维基百科](https://en.wikipedia.org/wiki/IOS#Kernel))

这是Mavericks用的kernel版本, 13.0.2.


{% highlight bash %}
	
% uname -v
Darwin Kernel Version 13.0.2: Sun Sep 29 19:38:57 PDT 2013; root:xnu-2422.75.4~1/RELEASE_X86_64

{% endhighlight %}

它们主流的开发语言都是Objective-C, 大部分Framework和Library也是通用的, 如Foundation/CoreFoundation, 就算不通用, 它们的设计也基本一致, 如UIKit/AppKit, 还有[Chameleon](http://chameleonproject.org/)这种致力于把UIKit搬到Mac的项目.

iOS下可用的[Framework列表](http://theiphonewiki.com/wiki//System/Library/Frameworks), 在`/System/Library/Frameworks`下可以找到.

文件系统目录结构一致, 默认用户是`mobile`; 越狱后的iOS才能算完整的Unix-like系统, 你可以装shell, terminal, 开ssh, 启后台进程, 绕过sanbox, 使用root权限, 使用动态库等等, Mac/Unix的知识全都可以用上.

正统的iOS App开发直接看Apple的[iOS App Programming Guide](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html)即可. 

一般而言, 你需要一台Mac进行正儿八经的开发, iDevice不是必需的. 但如果是开发越狱App, 你需要一台越狱后的iDevice, Mac反而不是必需的.

主要的开发环境有两种:

###On device toolchain 

最早的toolchain都是自己build的, 大神们的toolchain一般也不公开, 现在情况好一些, 直接装Bigboss提供的即可. 

这种做法好处是兼容性好, 测试方便, 比如你要编译个python的什么库; 

缺点也有不少, 由于不能自定义固件了, 系统区的空间比较少, 编译速度慢, 如果升级iOS并重新越狱的话又得再装一遍环境.

我第一个SBSetting toggle就是用iphone-gcc编译的~

对比表格来自[iPhone Dev Wiki](http://iphonedevwiki.net/index.php/On-device_toolchains)

<table class="wikitable">

<tbody><tr>
<th>
</th>
<th> iphone-gcc
</th>
<th> LLVM+Clang for iOS
</th></tr>
<tr>
<td> <b>iOS SDK tools version</b>
</td>
<td> 2.0
</td>
<td> 6.1
</td></tr>
<tr>
<td> <b>Maximum iOS SDK supported</b>
</td>
<td> 3.2
</td>
<td> 7.0
</td></tr>
<tr>
<td> <b>Supported ARCHS</b>
</td>
<td> arm, armv4t, armv6
</td>
<td> armv4t, armv6, armv7, armv7f
</td></tr>
<tr>
<td> <b>Compiler Version</b>
</td>
<td> GCC 4.0
</td>
<td> LLVM 3.3
</td></tr>
<tr>
<td> <b>CC Tools Version</b>
</td>
<td> 286
</td>
<td> 839
</td></tr>
<tr>
<td> <b>Cydia Repo Hosted On</b>
</td>
<td> Telesphoreo
</td>
<td> BigBoss
</td></tr>
<tr>
<td> <b>Last Updated On</b>
</td>
<td> July, 2008
</td>
<td> October, 2013
</td></tr>
<tr>
<td> <b>Maintainer</b>
</td>
<td> saurik
</td>
<td> coolstar
</td></tr>
<tr>
<td> <b>Default Target</b>
</td>
<td> arm-apple-darwin9
</td>
<td> armv7-apple-darwin11
</td></tr>
<tr>
<td> <b>ARCH built for</b>
</td>
<td> arm
</td>
<td> armv7
</td></tr>
<tr>
<td> <b>C++ version supported</b>
</td>
<td> C++98 (from 1998)
</td>
<td> C++11 (from 2011)
</td></tr>
<tr>
<td> <b>Obj. C Version supported</b>
</td>
<td> 2.0
</td>
<td> 2.0
</td></tr>
<tr>
<td> <b>Obj. C Blocks (4.0 SDK+) Supported?</b>
</td>
<td> No
</td>
<td> Yes
</td></tr>
<tr>
<td> <b>Obj. C ARC (5.0 SDK+) Supported?</b>
</td>
<td> No
</td>
<td> Yes
</td></tr>
<tr>
<td> <b>Obj. C Literals+Autosynthesize (5.1 SDK+) Supported?</b>
</td>
<td> No
</td>
<td> Yes
</td></tr></tbody></table>

###Cross compile

交叉编译的话, 主要就是[Theos](https://github.com/DHowett/theos)了, 它是跨平台的一套Makefile, 依赖perl, 在iOS也可以用. 

在Theos之前, 你需要手写Makefile, 麻烦不说还容易出错, 还需要自己设置各种环境变量/Flag. 比如最这个[Makefile](https://github.com/goagent/goagent-ios/blob/master/goagent-toggle/backup/Makefile.raw)

Theos的`nic`命令可以生成很多类型的模板, 主流的都包括了: 

	% theos/bin/nic.pl
	NIC 2.0 - New Instance Creator
	------------------------------
  	[1.] iphone/application
  	[2.] iphone/flipswitch_switch
  	[3.] iphone/library
  	[4.] iphone/preference_bundle
  	[5.] iphone/tool
  	[6.] iphone/tweak

简单的解释一下:

* ####application
正常的App, 在Mac下其实意义不大, 因为你可以直接用XCode

* ####tool
non-GUI工具, 比如写个helper或者daemon什么的.

* ####library
dylib或者Bundle

* ####flipswitch_switch
flipswtich的模板, ControlCenter插件.

* ####preference_bundle
Preference插件, 依赖Preference Loader, 插在Settings.app里.

* ####tweak
MobileSubstrate插件, 现在叫[CydiaSubstrate](http://www.cydiasubstrate.com/).
一般意义上的tweak大部分都是这类.

SBSettings Toggle/Preference Bundle/NotificationCenter Widget/FlipSwtich
这些插件都是动态库. 关于动态库, 推荐Apple的这篇:[Dynamic Library Programming Topics](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/DynamicLibraries/000-Introduction/Introduction.html).

CydiaSubstrate则是一个代码注入平台, 动态加载并注入dylib, 一般会和classdump/method swizzling配合, 具体可以看看它的[文档](http://www.cydiasubstrate.com/inject/darwin/), iPhone Dev Wiki上的[介绍](http://iphonedevwiki.net/index.php/MobileSubstrate)也不错.

更多的一些Tweak例子可以参考[Ryan Petrich's Tweak Week](http://tweakweek.com/).

#####Updates: 还可以试试[iOSOpenDev](http://www.iosopendev.com/), 我最早装过它的公测版, 当时有bug没用起来, 现在看上去可用多了.

####关于Root privilege

如何像Cydia那样以Root权限运行呢?

和传统做法基本一致:

1. 给你的executable加上`setuid/setgid bits`, 比如说在`postinst`脚本里加上: `chmod 6755 /path/to/executable`
2. 程序启动的时候调用`setuid(0)`
3. iOS不允许直接以root权限运行, 所以还要一个exec trick.

关于什么是setuid/setgid, 请直接`man chmod`并搜索`set-user-ID-on-execution`

具体可以看GoAgent iOS的这几个文件:[postinst](https://github.com/goagent/goagent-ios/blob/master/package/DEBIAN/postinst#L20), [main.m](https://github.com/goagent/goagent-ios/blob/master/goagent-ios/goagent-ios/main.m#L17), [goagent](https://github.com/goagent/goagent-ios/blob/master/goagent-ios/goagent-ios/goagent#L4), [Makefile](https://github.com/goagent/goagent-ios/blob/master/Makefile#L38)

还有种做法是利用launchd来执行需要root权限的操作. 从权限隔离的角度而言, 这种做法更好, 就是有点绕.

###关于launchd/launchctl

launchd是iOS/OS X的关键程序, 类似于init/upstart, 用来管理所有的进程. 你在Activity Monitor随便找个进程, 它的直接或者间接父进程都是launchd.

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/active_monitor_view_hierarchically_zpsbe835ca2.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/active_monitor_view_hierarchically_zpsbe835ca2.png" max-widght="100%" border="0" alt=" photo active_monitor_view_hierarchically_zpsbe835ca2.png"/></a>

launchd托管了很多job, 它们可以是进程, 可以是Timer; launchd还可以监控文件, socket等等. 功能相当强大, 更多可以查看手册:`man lauchd.plist`.

launchctl是launchd的命令行管理工具, 这次iOS7完美越狱也用到了([Shebang Trick](http://theiphonewiki.com/wiki/Shebang_Trick)).

launchd/launchctl是[开源的](http://www.opensource.apple.com/source/launchd/), 如果你想通过写代码来控制, 可以参考launchctl的实现.

顺带提一句, 现在GoAgent的[启动](https://github.com/goagent/goagent-ios/blob/master/goagent-local/org.goagent.local.ios.plist)/[停止](https://github.com/goagent/goagent-ios/blob/master/goagent-local/org.goagent.local.ios.stop.plist), 也是通过launchd的两个job实现的.

###bypass iPhone_NA

有时候你会看到这样的宏:

{% highlight c %}

__OSX_AVAILABLE_STARTING(__MAC_10_1,__IPHONE_NA);

{% endhighlight %}

它说明这个API仅在10.1之后的OS X下可用, iOS上不可用, 直接调用它编译器会报错. 

如何绕过呢?

我们是可以动态加载lib的, 利用dlopen/dlsym(上面的动态库介绍有详细介绍)即可:

{% highlight c %}

void* libHandle = dlopen("/System/Library/Frameworks/SystemConfiguration.framework/SystemConfiguration", RTLD_LAZY);

CFStringRef(*_SCDynamicStoreKeyCreateProxies)(CFAllocatorRef)
    = dlsym(libHandle, "SCDynamicStoreKeyCreateProxies");

//调用_SCDynamicStoreKeyCreateProxies

{% endhighlight %}

还有一种做法是AppProxyCap这种, 链接`SystemConfiguration.framework`之后直接[取地址](https://github.com/freewizard/AppProxyCap/blob/master/lib/AppProxyCap.m#L85):

{% highlight c %}

typedef CFDictionaryRef (*_SCDynamicStoreCopyProxies) (SCDynamicStoreRef store);
static _SCDynamicStoreCopyProxies origin_SCDynamicStoreCopyProxies;

origin_SCDynamicStoreCopyProxies = &SCDynamicStoreCopyProxies;

{% endhighlight %}

这种做法也可以用来判断OS版本, 比如某个API是5.0之后加入的, 那么之前的版本取地址将会得到空值.

#####Updates: 还可以把这个宏给undef掉~

###bypass sandbox

直接安装到`/Applications`即可.

###bypass codesign

直接看Saurik的这篇文章即可:[Bypassing iPhone Code Signatures](http://www.saurik.com/id/8), 有证书的话还是签下名吧.

###SSH Tips

* 记得把默认的`alpine`密码改掉, iOS下也是有病毒的:[ikee](http://www.f-secure.com/v-descs/worm_iphoneos_ikee.shtml)
* 没有WiFi的情况下, 可以考虑ssh over usb, 具体可以看[这里](http://iphonedevwiki.net/index.php/SSH_Over_USB)

* 开启ssh公钥认证, 可以节省很多时间, 比如Theos的make install和scp就不用输密码了.

* 顺带提下, 我的[vim-config](https://github.com/hewigovens/vim-config/blob/master/scripts/install_ios_configs.sh)也基本支持iOS, 主要是.vimrc/.bashrc

###Cydia Repo Hosting

Cydia的source/repo基本上是Debian的APT repo, 只需要提供:

1. Release, repo描述文件
2. Packages|Pacakges.gz/bz2, repo的package清单
3. *.deb, 实际package文件

Release文件几乎不用改, 只要准备好deb文件, 然后用`dpkg-scanpackage`命令生成Packages就可以了, 比如`update_packages.sh`:

{% highlight bash %}

#!/bin/bash
dpkg-scanpackages . > Packages && gzip -c Packages > Packages.gz

{% endhighlight %}

之后可以通过rsync同步到服务器上, 跑个文件下载的web服务就可以了, 比如当初学node写的`serve_cydia.js`, 依赖`node-static`:

{% highlight js %}

#!/usr/bin/env node

var node_static = require('node-static');
var http = require('http');
var url = require('url');

var cydia_files = new(node_static.Server)('./files');

http.createServer(function(request, response) {
	request.addListener('end', function() {
		if (request.url.search('cydia') === -1) {
			console.error('non cydia request:' + request.url +' from ' + request.connection.remoteAddress)
			return
		}
		cydia_files.serve(request, response, function(error, result){
			if (error) {
				console.error('' + request.connection.remoteAddress + ' ' + request.method + ' ' + request.url + ' ' + error.status + ' ' + error.message);
				response.writeHead(error.status, error.message);
				response.end();
			} else {
				console.log('' + request.connection.remoteAddress + ' ' + request.method + ' ' + request.url);
			}
		});
	});
}).listen(80)

{% endhighlight %}

不想自己hosting的话, 可以提交给[Bigboss](http://thebigboss.org/)或者是尝试下[myrepospace](http://www.myrepospace.com/).

###一些参考资源

* [Cydia Dev FAQ](http://cydia.saurik.com/faq/developing.html)
* [iPhone Dev wiki](http://iphonedevwiki.net/index.php/Main_Page)
* [the iPhone wiki](http://theiphonewiki.com/wiki/Main_Page)
* [Saurik's blog](http://www.saurik.com/)
* [Theos](https://github.com/DHowett/theos)
* [Ryan Petrich's Tweak Week](http://tweakweek.com/)
* [JailbreakQA](http://www.jailbreakqa.com/)
* [OpenJailbreak](https://openjailbreak.org/)
* [大神们的Twitter列表](https://twitter.com/hewigovens/jailbreak-hackers/members)
* [之前整理的wiki](https://github.com/hewigovens/hewigovens.github.com/wiki/Develop-Jailbreak-Apps)
* Books:
* * [iOS Hacker's Handbook](http://www.amazon.com/iOS-Hackers-Handbook-Charlie-Miller/dp/1118204123)
* * [Hacking and Securing iOS Applications](http://shop.oreilly.com/product/0636920023234.do)

--END

====