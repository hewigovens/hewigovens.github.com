---
layout: post
title: "recent interesting things about Objective-C/Cocoa"
description: ""
category: 
tags: ["cocoa","objective-c","mac"]
---
{% include JB/setup %}

最近看到一些有趣的, 和Objective-C/Cocoa有关的事情. 
***
### ▶ [Objective-C hackathon](https://objectivechackathon.appspot.com/)

这次hackathon的口号很有意思:叫"Back on the map", 在最近TIOBE的排名中, Objective-C的排名一直很高. 

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/Tiobe_20130711_zps725e3b02.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/Tiobe_20130711_zps725e3b02.png" border="0" alt=" photo Tiobe_20130711_zps725e3b02.png"/></a>

不过最近Github的Top Languages列表里, CoffeeScript把Objective-C的前十给挤掉了,这就是口号的由来~, 于是Cue就发起了这次hackathon.

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/TopLang_20130711_zps37614a82.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/TopLang_20130711_zps37614a82.png" width=100% border="0" alt=" photo TopLang_20130711_zps37614a82.png"/></a>

现在可以在([Objective-C Hackathon: Recap](http://tech.cueup.com/blog/2013/07/01/objective-c-hackathon-recap))查看结果

这篇blog中有类似编辑选择奖的东西, 其中就有[Mattt Thompson](https://github.com/mattt), 我也是最近才认识到这位大神的, 他是[Heroku](https://www.heroku.com/)的Mobile Lead, 在Github上非常活跃, 参加的组织高达11个, 著名的AFNetworking就是出自他手, 还有[Nomad-CLI](http://nomad-cli.com/), 和[Helios](http://helios.io/), 这两个的项目主页创意都非常棒, 尤其是nomad, cupertino->houston->dubai->venice->shenzen,从库布提诺到深圳, 串成了完整的"生态链", 壮哉我天朝大寨都~

组织的[Cue](https://www.cueup.com/)也值得一提, 早在他们还叫[Greplin](http://www.greplin.com)的时候我就了, 现在的Cue不但打磨的更漂亮, 还有着更大的愿景:
>Know what's next.

不过对我来说最有用的还是能够搜索自己的各种数据吧, 非公开的个人搜索引擎和Google刚好形成了互补, 不过Google其实也知道你这些数据吧...


### ▶ [Kaleidoscope](http://www.kaleidoscopeapp.com/)

Kaleidoscope是一个光看介绍就觉得像神器, 长久以来难求的Diff工具: 支持文件/文件夹比较, 甚至还支持图片; 漂亮的图标和界面; 支持命令行, 支持各种VCS, 就连名字都那么不俗; 它的[twitter账号](https://twitter.com/kaleidoscopeapp)还写着 "The world's most advanced file comparison application.", 的确不是滥得虚名. 我曾经用过的FileMerge/DiffMerge/P4Merge/Wine+BeyondCompare与之相比简直就是lamware. 70$绝对是物有所值.

硬要说美中不足的话, 就是好像不支持比较的时候忽略空格/空白行/制表符? 

KaleidoScope的背后是[Black Pixel](http://www.blackpixel.com/), 他们的另一产品[Versions](http://versionsapp.com/)光看介绍也觉得像神器, 不过我基本不用svn, 所以就没有试了. Black Pixel除了做产品, 还提供Service, 从前到后都会的顶级工作室. 

我是从这篇[blog](http://blackpixel.com/blog/2013/04/interview-questions-for-ios-and-mac-developers-1.html)了解到Black Pixel的:
>At Black Pixel, most of the developers on our staff have 7 to 10 years of Cocoa experience, and many of them are ex-Apple product engineers. The few 'junior' developers we have would be considered very senior anywhere else.

这就是我说顶级的原因了, 从blog中的问题来看, 还有很多我没怎么接触的Framework, 比如Core Animation/Graphics.

Black Pixel的[团队介绍](http://blackpixel.com/team.html)也很有意思:
>Not just a majestic shaolin temple renowned for its kung fu fighting monks.

自比为少林的高手的大胡子们~


### ▶ [Plausible Labs](http://www.plausible.coop/software)

和Black Pixel很像, Plausible Labs也是一家很酷的工作室, 号称什么都能做(servers, operating systems, graphics pipelines, audio processing), 开发了很多著名的应用和开源类库:

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/PJLabs_20130711_zpsf42f6e31.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/PJLabs_20130711_zpsf42f6e31.png" width=100% border="0" alt=" photo PJLabs_20130711_zpsf42f6e31.png"/></a>

HockeyApp, Atlassian JMC和Flurry都用到了[PLCrashReporter](https://www.plcrashreporter.org/), 肯定是比iTunes Connect.

[PLBlocks](https://code.google.com/p/plblocks/), 当时也想做类似的东西的. 最后还是放弃在10.5上用block了, 如果当时知道它, 说不定就用上了~
>Block-capable Toolchain/Runtime for Mac OS X 10.5 and iPhone OS 2.2+


[PLActorKit](https://code.google.com/p/plactorkit/)看上去还不错, 不过好像是用pthread实现了actor模型? 

***

有时候你真的会很羡慕这些家伙, 兴趣驱动, 良好的氛围, 光是看到这些也能感受到他们的技术热情, 这也难怪国外会有很多"高龄"程序员吧, 或许就像就像Matt在自己[blog](http://mattt.me/2012/open-source-and-commercial-support/)里说的那样, Code is our passion.

The End.