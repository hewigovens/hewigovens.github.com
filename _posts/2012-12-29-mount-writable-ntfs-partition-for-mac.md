---
layout: post
title: "Mac下挂载可写NTFS分区"
description: ""
category: 
tags:
- mac
---
{% include JB/setup %}

---

在Mac下, 默认挂载的NTFS分区是只读的, 有时候会很不方便. 商业的解决方案有￼￼[Tuxera](http://www.tuxera.com/products/tuxera-ntfs-for-mac/)和[Paragon](http://www.paragon-software.com/home/ntfs-mac/), 开源的就是[ntfs-3g](http://macntfs-3g.blogspot.com/)和[FUSE for OSX](http://osxfuse.github.com/)了(MacFUSE的继任者~). 折腾过Linux的同学应该很熟悉他们了.

###安装步骤:

1. 下载[ntfs-3g-2010.10.2-macosx.dmg](http://sourceforge.net/projects/catacombae/files/latest/download?source=dlp), 打开并安装, 记得勾掉"MacFUSE".
2. 下载[OSXFUSE-2.5.4.dmg](https://github.com/downloads/osxfuse/osxfuse/OSXFUSE-2.5.4.dmg), 打开并安装, 注意记得勾上"MacFUSE Compatibility Layer". 原因是ntfs-3g的版本比较老, link的还是MacFUSE的libary.
3. 如果是10.7以后的系统, 还需要下载[fuse_wait-1.1.pkg](https://github.com/downloads/bfleischer/fuse_wait/fuse_wait-1.1.pkg)并安装. 这是个workaround, 具体可以看[这里](https://github.com/bfleischer/fuse_wait/blob/master/README.md)

###Reference:

[NTFS-3G for Mac OS X](https://github.com/osxfuse/osxfuse/wiki/NTFS-3G)