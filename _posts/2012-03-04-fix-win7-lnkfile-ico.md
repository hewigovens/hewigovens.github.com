---
comments: true
date: 2012-03-04 20:39:50
layout: post
slug: fix-win7-lnkfile-ico
title: 修复win7图标异常
wordpress_id: 541
categories:
- Tricks
- Windows
tags:
- Windows
---

某天突然发现桌面图标异常了：





<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2012/03/44f79696gw1dq8y001ibcj_zps7448da15.jpg.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2012/03/44f79696gw1dq8y001ibcj_zps7448da15.jpg" border="0" alt=" photo 44f79696gw1dq8y001ibcj_zps7448da15.jpg"/></a>





清理了桌面图标缓存也没有效果，想到桌面图标基本上是注册表HKEY_CLASSES_ROOT\lnkfile控制，报着试试的想法，备份了下HKEY_CLASSES_ROOT\lnkfile的所有键值，然后删除之，重启explorer。很好，桌面图标都打不开了，再重新导入刚刚备份的reg文件，再重启explorer，奇迹般的好了~





<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2012/03/2_zps57c1d22f.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2012/03/2_zps57c1d22f.png" width=100% border="0" alt=" photo 2_zps57c1d22f.png"/></a>



