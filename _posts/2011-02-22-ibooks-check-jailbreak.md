---
comments: true
date: 2011-02-22 21:34:50
layout: post
slug: ibooks%e7%9c%9f%e7%9a%84%e6%a3%80%e6%b5%8b%e8%b6%8a%e7%8b%b1%e4%ba%86
title: iBooks真的检测越狱了
wordpress_id: 198
categories:
- iOS
- Tricks
tags:
- iOS
- jailbreak
---

前段时间看[新闻](http://www.weiphone.com/apple/news/2011-02-16/Apple_iBooks_in_the_latest_version_of_the_anti-escape_measures_added_230787.shtml)，听说新版的iBooks加入了检测越狱的代码，原理和反向继电器挺像的，接电反而断开：在载入任何受数字版权保护的图书前（例如你从iBookstore里购买的任何图书），iBooks会尝试运行一小段代码。未越狱的系统由于用户没有足够的权限，会拒绝运行这个程序，iBooks侦测到这个异常反而会正常启动。而经过越狱的系统默认情况下会运行这个程序，没有检测到异常的iBooks便拒绝启动。结果我今天碰到了：

[![IMG_0140](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0140_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0140.png)[![IMG_0137](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0137_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0137.png)

正好刚刚刷cydia的package时看到comex的破解补丁，于是安装之，再打开就好了，comex果然是大神，而且还那么年轻，看看人家，不提也罢。

[![IMG_0138](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0138_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0138.png)[![IMG_0139](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0139_thumb.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/02/IMG_0139.png)
