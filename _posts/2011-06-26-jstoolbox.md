---
comments: true
date: 2011-06-26 23:12:42
layout: post
slug: jstoolbox
title: JSToolbox
wordpress_id: 267
categories:
- Javascript
- Tricks
---

最近写了个Greasemonkey脚本[jstoolbox](http://userscripts.org/scripts/show/105562)，将一些bookmarklet（爱库，QQ输入法，有道翻译，Instapaper）做成了一个下拉列表，在页面顶上就能点击使用。为什么要多此一举呢？点书签不是很方便吗？原因其实是在我使用Firefox的时候，只会保留地址栏、Tab栏、和右下角的扩展栏，没有书签栏；而且我多年的收藏经验表示，我最讨厌点击书签了，收藏夹里的书签基本上没点过，一是数量比较大，组织的麻烦，二是收藏夹每次打开都是密密麻麻的，根本不想细看。直到我发现了[Fastdial](https://addons.mozilla.org/en-US/firefox/addon/fast-dial-5721/)，不点收藏夹的情况才有所改观。快速拨号这个功能最早是opera发明的，Firefox上也有很多扩展，但是都用的不太顺手，Fastdial有点不一样，很简单，如同它的名字一样，打开速度很快，支持文件夹的功能，生成的缩略图基本上不看标题也知道是什么网站，而且对应到收藏夹里就一个Fastdial的文件夹，所以我就把Fastdial当成收藏夹来用了。

 

这个问题一直存在就对了，不过真正让我写脚本的原因是爱库的Firefox扩展，[爱库网](http://ikeepu.com/)是一个用于整理（collect），组织（organize），分享（share）任何互联网上面的网站、图片、视频等资源的在线服务，并且致力于让用户发现（discover）更多有意思的互联网资源。而且爱库网收藏的内容都以缩略图的方式来展示这一点我很满意，为此我还弃用了delicious。安装爱库的Firefox扩展后，它会hook住新Tab的打开页面，效果是不错但是这样一来Fastdial就不能用了；而且必须要到菜单->工具才能点到爱库的选项。因为菜单栏一般都是隐藏的，所以就相当不爽了。好在爱库提供了一个bookmarklet，顺带我就把其他的一些我觉得有用的bookmarklet给加进来了，代码也很简单，把li元素createElement出来，然后绑定上对应的function，最后添加到当前页面。因为bookmarklet其实就是浏览器执行一段js，所以那些function其实就是bookmarklet。目前已知的问题是在一些web mail里，如网易邮箱会被insert多次，所以把网易邮箱添加到了exclude里。

 

效果图如下：

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/06/image_zps36d56bd3.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/06/image_zps36d56bd3.png" border="0" alt=" photo image_zps36d56bd3.png"/></a>

 

鼠标移到JS-Toolbox会出现一个下拉列表，点击即可。

 

<a href="http://s750.photobucket.com/user/hewigovens/media/wp-migrate/uploads/2011/06/image1_zps674649fc.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/wp-migrate/uploads/2011/06/image1_zps674649fc.png" border="0" alt=" photo image1_zps674649fc.png"/></a>

 

后续可能的工作：1.添加别的功能，现成的bookmarklet或者其他的js小工具。2.修改代码使得易于修改配置，可以选择哪些打开，哪些关闭。
