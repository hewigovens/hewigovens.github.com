---
layout: post
title: "从Evernote到Trello"
description: ""
category: 
tags: ["trello", "evernote"]
---
{% include JB/setup %}

Trello是Joel Spolsky(软件随想录作者, StackOverflow创始人之一)基于[看板](https://en.wikipedia.org/wiki/Kanban)理论开发的项目管理网站, 口号是"Organize anything, together"; Evernote是著名的笔记工具, 口号是"Remember everything". 按理说两者定位不同, 没什么可比性, 由于我用Evernote始终觉着不爽, Trello又很对我的胃口, 所以打算把Evernote里的东西都移动到Trello.

下面是一些我觉得有用的一些工具:

###[Boards for Trello](https://chrome.google.com/webstore/detail/boards-for-trello/eknhddnoflchkcccjgdddmnimjggiona)

Chrome Extension, 列出你所有Board, 可以比较便捷的导航.

###[Trello-Bookmarklet](https://github.com/hewigovens/Trello-Bookmarklet)

Bookmarklet, 快速创建卡片, 除了支持FogBugz/JIRA/Github的case页面外, 还支持从任意页面选中的内容创建. 配合[SpellBook](https://chrome.google.com/webstore/detail/ihckioenbbjedpocnnennnehjaacojil)效果极佳. 
原来的Trello-Bookmarklet选择卡片列表的时候会把已经关闭的Board也列出来, 所以我fork了一份, 会过滤掉已经关闭的Board. 这里要吐槽一下, Trello的Board/List目前是不能删除的, 只能Archive.

这个就是选中一段文字创建的:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/trello_card_wide_zps02375d86.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/trello_card_wide_zps02375d86.png" width="100%" border="0" alt=" photo trello_card_wide_zps02375d86.png"/></a>


###[Card this to Trello](https://chrome.google.com/webstore/detail/trello-this/llapjidoaciepmfjchefhhachlmehfdl)

Bookmarklet还是有些不爽, 于是我又搞了个Chrome Extension, 主要改进在于:

* 不用输多次App Key了
* 添加了右键菜单, 不需要SpellBook也可以了
* 把原来的通知改成了Desktop Notification

###[Wider Trello Card](http://userstyles.org/styles/92916/wider-trello-card)

细心的同学可能发现了, 上面那张截图似乎有点宽? 这是因为我觉得Trello默认的卡片宽度有点窄, 文字一多就看着不太舒服, 所以就写了这个user style脚本, 把卡片的宽度给加大了200px. 顺带提一句, Trello卡片是支持Markdown的, Evernote至今还不支持.


最后, Trello的移动客户端体验也不错, 很喜欢卡片这种设计, 简单而又一目了然. [这里](https://trello.com/docs/#tools-and-projects-using-the-api)能看到更多的工具, 如果没有满意的, 还可以考虑自己动手利用Trello开放的[API](https://trello.com/docs/gettingstarted/index.html)来实现.

--End
