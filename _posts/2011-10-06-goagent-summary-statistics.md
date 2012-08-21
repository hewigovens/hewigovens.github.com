---
comments: true
date: 2011-10-06 16:47:19
layout: post
slug: goagent-summary-statistics
title: GoAgent小结--统计篇
wordpress_id: 366
categories:
- Python
tags:
- goagent
- python
---

GoAgent 发布快半年了，打算写两篇小结一下，[另一篇](http://kernelpanic.im/blog/2011/10/08/goagent-summaries-technical/)会讲技术相关的内容~

如果没有最开始的随意[发布](http://internet.solidot.org/article.pl?sid=11/04/11/014244)，GoAgent 或许还只是个内部使用的小玩意，这是当时的新闻：
[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/solidot_news.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/solidot_news.png)

而现在，GoAgent 在Google Code上star数超过了850，issue数超过了1000，

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/goagent_star.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/goagent_star.png)

这实在是有点意外，不信可以看看上千的都是什么project，CyanogenMod也不过860而已：

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/famous_stars.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/famous_stars.png)

在Google Trends搜索流行度已经超过了老前辈gappproxy。[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/trends.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/trends.png)

和最流行的目田门相比，差距也有变小的趋势。

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/trends2.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/trends2.png)

根据Google Analytics 最近三个月的统计，GoAgent 首页PV有23W，独立访问才3.8W，可以推测除了作者之外，有人也每天刷GoAgent的首页。。中间的peak貌似是宣布支持iOS的时候，九月底的另一个peak貌似是支持php的延后效应。

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/overview.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/overview.png)

GoAgent 的下载数和用户数很难估计，因为github并没有下载的统计，很多人更新GoAgent也是git remote update这种方式，而且下载了并不代表就会使用。几万用户估计应该有，分布在“全球”。。

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/vistors.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/vistors.png)

很显然，Windows和Chrome用户是主流。

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/browsers_os.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/browsers_os.png)

GoAgent iOS好一点，提供了Google Code和cydia源的下载，结合Google code和这个简单的[脚本](https://gist.github.com/1266796)进行统计，GoAgent iOS大概下载了1500次，而python2.6下载2200次左右，用户数应该不到1千。。

[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/goagent_ios_down.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/goagent_ios_down.png)

GoAgent 的搜索流行度得到了Google Analytics数据的支持，一半以上流量都是通过搜索而来，说明在首页放置下载链接和Google +1是相当正确的。[![](http://kernelpanic.im/blog/wp-content/uploads/2011/10/search_traffic.png)](http://kernelpanic.im/blog/wp-content/uploads/2011/10/search_traffic.png)

顺带提下，还有个ezproxy的事情，具体可以看v2ex的[帖子](http://www.v2ex.com/t/13674)和这个[链接](http://www.ufula.com/vip.html)，我根据淘宝显示的最近成交记录估算了一下，那个哥们利用GoAgent赚了大概1000块，不过这也从侧面证明了GoAgent的速度和可用性，都可以拿来卖钱了~


