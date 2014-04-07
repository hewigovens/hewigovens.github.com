---
layout: post
title: "GhostTile, 隐藏Dock上运行App"
description: ""
category: 
tags: ["OS X", "Dock"]
---
{% include JB/setup %}

这个想法2月底就冒出来了, 当时快速的验证了下, 还是比较可行的. 最近利用业余时间折腾了下, 发布了第一个正式beta版.

如果你是Dock隐藏党或者Afred/Launchbar党, 可能会觉得没什么用. 但是每个人的习惯和用法不一样, 我从去年就踏上了自制各种工具的不归路, 所以就按自己的习惯写了一个.

我习惯于⌘+Tab, 习惯于正下方的Dock, 如果程序开的多, ⌘+Tab切起来效率就直线性下降了. 
对于有些实际上只在后台使用的应用, 比如Vox, TunnelBear. 或者是只需要偶尔切换到前台的如词典, HockeyApp之类的, 希望它们不要出现在⌘+Tab列表里但是又能够快速切到前台.

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/boincmanager_dock_icon_zps3c157cec.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/boincmanager_dock_icon_zps3c157cec.png" border="0" alt=" photo boincmanager_dock_icon_zps3c157cec.png"/></a>

这个大家都不陌生吧, 我忍它很久了.

早期其实有类似的一些工具, 比如Dock Dodger和MenuAndDockless. Dock Dodger本质上是修改应用的配置文件, 对于sign过的基本上就跪了. 而MenuAndDockless是SIMBL的插件, 光看截图就觉得很复杂. 所以对比起来GhostTile还是有一些技术上的优势的:

* 基本零配置, 无外部依赖
* 支持sign过的, sandbox过的应用, 不会去修改本地磁盘上的文件
* 提供快捷键支持, 可用性不错

下面是一些截图:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/ghosttile_main_window_zps62d9acd0.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/ghosttile_main_window_zps62d9acd0.png" max-width=100% border="0" alt=" photo ghosttile_main_window_zps62d9acd0.png"/></a>

主界面

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/ghosttile_quickswitch_window_zpsf722a389.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/ghosttile_quickswitch_window_zpsf722a389.png" max-width=100% border="0" alt=" photo ghosttile_quickswitch_window_zpsf722a389.png"/></a>

快速切换界面

图标是一个叫萌萌的萌妹子帮我设计的, 另外为了捞回开发者账号的钱, GhostTile定价9.99$, 不过实际上没有试用时间的限制, 做法和Sublime差不多, 最多提示一下.

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/ghosttile_promote_alert_zps914f0dae.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/ghosttile_promote_alert_zps914f0dae.png" max-width=100% border="0" alt=" photo ghosttile_promote_alert_zps914f0dae.png"/></a>

购买提示

我分别上传了Demo视频到Youtube和Youku, 有条件的还是看Youtube吧.

* [https://www.youtube.com/watch?v=oZ6iX83i32E](https://www.youtube.com/watch?v=oZ6iX83i32E)
* [http://v.youku.com/v_show/id_XNjk1MjIzNjY4.html](http://v.youku.com/v_show/id_XNjk1MjIzNjY4.html)

欢迎大家测试beta版本, [戳这里](https://rink.hockeyapp.net/recruit/e9bc821fe40c4c379111a6dce31de812)的Request access应该就能下载beta版了.

附上GhostTile的tumblr主页: [http://ghosttile.kernelpanic.im/](http://ghosttile.kernelpanic.im/)

