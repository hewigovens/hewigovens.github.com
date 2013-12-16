---
layout: post
title: "CopyMate小结"
description: ""
category: 
tags: ["copymate","keyboard","shortcut","Mac"]
---
{% include JB/setup %}

CopyMate是一个Mac剪贴板辅助工具，
虽然口号是*Copy Anywhere, Paste Once*，但是目前暂时只支持复制文本，只支持10.8以上系统；CopyMate 希望能够在如下场景中派上用场：

1. 从一段代码中选择性复制几行；作为一名主要靠复制粘贴吃饭的程序员(笑)，你肯定有过这种需求。
2. 从不同的应用程序中复制片段；比如浏览器复制链接，终端复制命令行，IDE复制代码，然后一次粘贴出来。

CopyMate的动机来源很简单：最近维护的一个项目是从Windows下移植过来的，代码很久没有同步了，现在要加点新功能，需要参考最新的Windows代码。得益于开源项目，最核心的功能一天就跑通了，UI，自动升级，自动打包发布反而花了更多的时间。

###屏幕取词

做的最好的应该是Apple自家的词典了，然后是Popclip，有道这种需要装插件的做法基本上不用考虑了。总结起来就是: 没有通吃的做法, 一般是各种方法组合:

>It uses various techniques to obtain the text from the application (Text
Service Manager and TSM Document Access CarbonEvents, along with
Accessibility APIs.)

参考[cocoabuilder的帖子](http://www.cocoabuilder.com/archive/cocoa/200106-reading-word-at-mouse-pointer-o-universal-access.html)

还有一种比较tricky的做法是模拟CMD+C，一开始我直接尝试`CGEventPost`没搞定，后来发现了[QuickCursor](https://github.com/jessegrosjean/quickcursor)，它的做法是利用Accessibility API来模拟CMD+C, Popclip在Sublime里也是这种做法. 所以就采用这种做法了, CopyMate本来也要读写粘贴板.

基本流程如下:

	快捷键 -> 读取剪贴板并保存 -> 模拟复制 -> 格式化 -> 写回剪贴板 -> 粘贴

###快捷键

用了[MASShortcut](https://github.com/shpakovski/MASShortcut)，顾名思义，能通过MAS审核的快捷键库. 但是CopyMate用了Accessibility API的好像就无法Sandbox了，还是会被MAS给reject掉. 为了显示快捷键的效果, 我特定
还录了一段demo视频, 用的ScreenFlow试用版, 编辑功能相当赞, 就是略贵.

###Build/Publish/Update

Build托管给了[Travis](https://travis-ci.org/hewigovens/copymate), 看见[![Build Status](https://travis-ci.org/hewigovens/copymate.png)](https://travis-ci.org/hewigovens/copymate)成功的标志心情大好. 

Travis现在已经越来越成熟了, 具体教程可以参考objc.io的这篇[教程](http://www.objc.io/issue-6/travis-ci.html), 写的很详细. 不过我遇到一个[xctool](https://github.com/facebook/xctool‎)的问题, 在本地xctool 1.4可以正常build, 在travis的xctool 1.3就一直失败, 无奈直接改用xcodebuild了. 

Publish的话, 集成了七牛存储, 只要你push一把, travis build成功之后会调用七牛的python sdk把zip包给上传上去. 你可以访问[http://dn-copymate.qbox.me/](http://dn-copymate.qbox.me/)来获取最新的build. 

七牛的文档上千叮万嘱你不用泄露app secret, 结果回头他自己就在travis的[log](https://travis-ci.org/qiniu/python-sdk/jobs/15213806)给泄漏了, ==!; 另外七牛给空间"自定义"404的功能也很弱, 自定义来自定义去还是只能文件名是`errno-404`, 而且不支持默认页面, 所以我把404页面当成首页来用了:显示最新build的下载地址, 这个404文件也是在travis build过程中生成上传到七牛的. 

升级的话, 集成了最流行的Sparkle, 这就不用多介绍了吧. 这里有个误区: Info.plist里的 `CFBundleShortVersionString`主要是用来给UI呈现用, 不应该用来实际判断版本高低, 举个例子, 每次OS X大版本升级, 总有些软件不兼容而被Apple给禁掉(一般会挪到这里: `/Incompatible Software`), 这个时候你更新`CFBundleShortVersionString`是没用的, 你需要更新`CFBundleVersion`, 而Sparkle正确处理了这个地方. 

Sparkle的feed放在github上了, 推送更新还是手动比较保险, 就没有放到build中去了.

最后这部分就是programming和engineering的区别了, Programming负责解决问题, Engineering的话还得包括其他部分. 

--End