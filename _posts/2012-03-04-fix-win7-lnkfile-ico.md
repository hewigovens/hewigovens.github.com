---
author: hewig
title: 修复win7图标异常
excerpt:
layout: post
category:
  - Tricks
  - Windows
tags:
  - Windows
post_format: [ ]
---
某天突然发现桌面图标异常了：

[![][2]][2]

清理了桌面图标缓存也没有效果，想到桌面图标基本上是注册表HKEY\_CLASSES\_ROOT\lnkfile控制，报着试试的想法，备份了下HKEY\_CLASSES\_ROOT\lnkfile的所有键值，然后删除之，重启explorer。很好，桌面图标都打不开了，再重新导入刚刚备份的reg文件，再重启explorer，奇迹般的好了~

[![][3]][3]

[![][4]  
][4]  

 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/44f79696gw1dq8y001ibcj.jpg
 []: http://kernelpanic.im/blog/wp-content/uploads/2012/03/2.png
 []: javascript: