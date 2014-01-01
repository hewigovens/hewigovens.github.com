---
layout: post
title: "我的2013"
description: ""
category: 
tags: ["life","retrospection","y2013"]
---
{% include JB/setup %}

2013年结束了, 翻了一下去年的计划和总结, 同样是感觉时光飞逝, 只是今年有种强烈的时不我待的感觉.

###关于阅读:

今年只读了6本:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/2013_year_end_reading_zps347ba3b5.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/2013_year_end_reading_zps347ba3b5.png" border="0" alt=" photo 2013_year_end_reading_zps347ba3b5.png"/></a>

统计来自[这里](http://www.mzread.com/annual_report/2013?include_douban=1)

对比下往年:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/2013_year_end_reading2_zpsa0c6d909.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/2013_year_end_reading2_zpsa0c6d909.png" border="0" alt=" photo 2013_year_end_reading2_zpsa0c6d909.png"/></a>

统计来自[这里](www.yuedudna.com/users/11396691/book/all_years)

正所谓买书一时爽, 搬家泪两行; 2013年印象中就没买过实体书, 12月初的时候还把海淘的DXG给卖掉了.

未来的阅读不会是实体书, 不会是Kindle, 至少不是DXG. 

我现在的阅读时间比较零碎的, 主要读全文RSS,邮件订阅,各种途径的推荐,PDF. 如果RSS不提供全文的就自己搞, 比如[yahoo pipes](http://pipes.yahoo.com/pipes/person.info?display=pipes&guid=VW7RWCXJFLGGS35XYOJ2DWC5XI)(是的, 它还活着), [fullrss.net](http://fullrss.net), 对于reddit这种就需要写代码了, 如[reddit-fun](https://github.com/hewigovens/reddit-fun), 托管在heroku上, 用readability的库抓全文, 输出score至少10的文章.

PDF的话主要用Adobe, 跨平台同步, 可以给PDF加标注. 以前学新技术喜欢看实体书, 现在的话直接看官方文档和例子, 然后上手折腾, 后面再补全知识.


###关于博客/Wiki

博客写了11篇, 技术性好像越来越低, 很多都进了wiki和Trello. 这次准备开一个坑, 打算写一系列介绍文章, 比如某个Mac App背后的公司.

今年花了不少功夫在Wiki上面, 用[GitStats](https://gitstats.sourceforge.net)统计了下: 

```
Project name:
	wiki
Generated:
	2014-01-01 13:30:17 (in 2 seconds)
Report Period:
	2012-10-20 08:30:29 to 2013-12-24 21:18:07
Age:
	431 days, 81 active days (18.79%)
Total Files:
	51
Total Lines of Code:
	1908 (2561 added, 653 removed)
Total Commits:
	316 (average 3.9 commits per active day, 0.7 per all days)
```
两千多行应该也不算少, 毕竟这不是代码.

加上了sidebar和footer, 是不是看上去专业不少?

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/2013_year_end_wiki_sidebar_zps3844b3be.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/2013_year_end_wiki_sidebar_zps3844b3be.png" border="0" alt=" photo 2013_year_end_wiki_sidebar_zps3844b3be.png"/></a>

###关于Weekend Project

今年略遗憾, 没有学习新的编程语言也没有参加新的MOOC. 倒是喜欢上了自制工具:

##### [CurrencyConvert](https://github.com/hewigovens/CurrencyConvert)
Popclip插件, 不同货币转换成人民币

##### [Card this to Trello](https://github.com/hewigovens/trello-this)
Trello-Bookmarklet的Chrome插件版本, 本来叫Trello This的, 后来Trello的一个哥们联系我说这个命名违反了ToS
    
##### [git-trello-hook](https://github.com/hewigovens/git-trello-hook)
github/gitlab webhook, 如果commit信息了有[card #1], 则会把trello的card给更新下, 现在配置略烦, 以后可以简化下
##### [PackageUninstaller](https://github.com/hewigovens/PackageUninstaller)
pkg卸载器, 之前有写博客介绍, 再要增强就得些kext了. 昨天[重构了一下](https://github.com/hewigovens/PackageUninstaller/commit/0df4db15fc06209ceb80f8ce9b8772d28a8d5e8e)是因为看到了这篇文章:[The code you wrote six months ago](http://blog.securemacprogramming.com/2013/06/the-code-you-wrote-six-months-ago/), 果然发现几个月前写的代码不忍直视...

##### [CopyMate](https://github.com/hewigovens/copymate)
剪贴板辅助工具, 之前也有介绍
##### [BookmarkSpell](https://github.com/hewigovens/BookmarkSpell)
Chrome插件, 最开始是想做成基于书签的Automator, 现在则是想自己帮助学习的知识管理系统, 其实我从来都不是学霸, 学习新东西能够带来给我带来乐趣就够了.自用了一段时间, 查了下DB, 有133条记录, 大部分是认真读过并且加了标签和笔记.

下一步准备自己搭server, 把数据从Dropbox Datastore迁移过来, 然后自己分词建索引, 实现全文搜索的功能. 

现在的样子:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/2013_year_end_bookmark_spell_zps536ef287.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/2013_year_end_bookmark_spell_zps536ef287.png" border="0" alt=" photo 2013_year_end_bookmark_spell_zps536ef287.png"/></a>

前几天写了个简单的Android客户端, 从手机上也可以容易的添加书签和笔记了:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/2013_year_end_bookmarkspell_android_zpsa309046f.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/2013_year_end_bookmarkspell_android_zpsa309046f.png" border="0" alt=" photo 2013_year_end_bookmarkspell_android_zpsa309046f.png"/></a>

###关于生活

Quora上面有不少有趣的问题, 比如[What are the best day to day time saving hacks?](http://www.quora.com/Productivity/What-are-the-best-day-to-day-time-saving-hacks), 可以直接看原文, 或者是[翻译版](http://blog.littlelin.info/posts/2013/12/04/quora-translation-what-are-the-best-day-to-day-time-saving-hacks), 最赞的是Marius Ursache的回答:

>**It's not about time. It's about energy.**

>We try to squeeze as many hours in one work day, to be "productive", but in the >end everything depends less on time, and more on your focus, motivation and overall well-being (all of them linked directly with energy levels).

我感触挺深, 这真是一针见血, 所谓的拖延症不就是low energy么; 除了作者提到的focus/motivation外, 我认为还有一点是ability, 很多时候拖延只是因为能力值不够而已. 


另外一个问题[How can I accelerate my personal growth](http://www.quora.com/Self-Improvement/How-can-I-accelerate-my-personal-growth)

最赞的是Jim Stone的回答:

>**In other words, choose "anxiety-driven growth" over "boredom-driven growth".**

<img src="http://qph.is.quoracdn.net/main-qimg-307add6b8883d02db6c1d174b791dbc9?convert_to_webp=true" />

这个图的横坐标是Skills, 纵坐标是Challenges. 从A1到A4就是提高的目标, 两种途径:

1. A1->A3->A4, 当前的Challenge超过当前的Skill, 这是*anxiety-driven growth*, 
2. A1->A2->A4, 当前的Skill超过当前的Challenge, 这是*boredom-driven growth*

一般*anxiety-driven*提高的更快, 这也取决与你是否能容忍远离你的舒适区, 以及能远离多远. 

这应该是我从南京->杭州的主要原因, 工作的本质或许没有改变(换个时间/路程变长的地方写代码), 但是环境的确变了.

最后是lifehacker的这篇:[7 Reasons You Haven’t Found Your Passion Yet](http://www.lifehack.org/articles/lifehack/7-reasons-you-havent-found-your-passion-yet.html)(纳豆有[翻译版](http://www.naadou.com/7-reasons-you-havent-found-your-passion-yet.html)). 

中枪不少, 生活就应该不断尝试.

###台湾之行

今年最值的应该是台湾之行了, 7天时间根本不够, 很多地方都没去成, 是我之前攻略的不够仔细和充分造成的; 旗津半岛给我们领路的大叔如是说: 年轻的时候没经验, 等到有经验的时候说明你已经老了. 重要的旅途的过程, 开心就好. 有机会一定要再去一次, 弥补一下.

###新年

新年的计划暂时还没想全, 但是有件事情一定要去做:把GoAgent iOS给重构下并支持iOS7,尽管现在没什么人在用了; 很多人都在讨论越狱还有没有意义, 输入法, 控制中心什么的系统都自带了, 我还是赞同@linusyang看法, 即现代越狱观(^_^), 追求自由是一种态度, 而且越狱对于我来说还有另外一层意义, 越狱后的iTouch3, 这是我最早接触的iOS开发环境, 第一个插件完全没有用Mac机器~

走出去多交流也很重要, 毕竟留给中国队的时间不多了.

--End

---