---
layout: post
title: "BookmarkSpell Introduction"
description: ""
category: 
tags: ["chrome", "bookmark", "extension", "javascript"]
---
{% include JB/setup %}

BookmarkSpell是一个Chrome的浏览器插件, 虽然号称理念是`bookmark based automator`, 但是目前已经实现的功能只是试图解决这篇[博客](http://www.kernelpanic.im/2013/05/03/collection-fragment-1/)提出的问题:基于浏览器书签的知识管理. 

BookmarkSpell监听了Chrome的书签事件, 在你保存之后会弹出一个窗口让你输入标签和笔记, 点OK之后会BookmarkSpell调用Readability的API来抓取全文并保存到Dropbox的Datastore里.

具体的代码和使用截图都放在[Github](https://github.com/hewigovens/BookmarkSpell/)上了, 第一次写Chrome插件, 遇到不少坑, 求轻拍. Chrome Store链接[在此](https://chrome.google.com/webstore/detail/hgimfomnnbecdjlndbhkcblaeoegpafn)

由于[Datastore API](https://www.dropbox.com/developers/datastore)还在Beta阶段, 并没有提供server端可用的SDK(我有尝试把JS的SDK放到nodejs的环境下跑, 可耻的失败了=_=!), 所以最重要的搜索功能还没实现.

其实有很多人吐槽这个没什么用, 可能他们并没有我这样的需求吧. 另一个原因是现在觉得很多服务都变的不可靠了, 比如上个月底, 我之前的主力笔记工具[Catch.com](https://catch.com/)宣布要[停止服务](http://support.catch.com/customer/portal/articles/1239367-catch-is-closing-down)了, 之前写的reddit feed也是, 试了很多App, 都不好用. 与其依赖于别人, 还不如自己动手.

