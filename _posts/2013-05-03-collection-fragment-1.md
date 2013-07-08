---
layout: post
title: "collection fragment 1"
description: ""
category: 
tags: ["collection"]
---
{% include JB/setup %}

一直觉得浏览器的书签收藏功能起不到知识管理的作用:

* 原有的链接可能会失效
* 添加起来,但是搜索起来很困难
* 不能添加notes
* 不能分类, 加tag
* Reader之后, 对各种服务的持久性产生了怀疑

各种各样的书签工具都用过, [Zootool](http://zootool.com/)和[爱库](http://ikeepu.com/)还有之前的[Delicious](https://delicious.com)注重social功能和预览图; [PearlTree](www.pearltrees)的可视化和分类管理做的很炫,但是维护起来麻烦. [historio.us](http://historio.us)很不错, 不过免费版只能添加50条书签, 要是能和PearlTree结合起来就好了.[Holmes](https://chrome.google.com/webstore/detail/holmes/gokficnebmomagijbakglkcmhdbchbhn)是chrome的搜索书签的一个插件, 比自带的要好用.

我期望的工具可能是更好的historio.us吧:

* 定期的sync chrome的bookmarks
* 浏览器插件添加书签的时候还能够edit, 添加注释和分类
* 更好的可视化展现
* 更可读导出和备份格式, 不喜欢bookmark.htm这种
* 开源, 能够自己搭建服务

暂时只想到这些, 为了以后能够容易的导入导出, 打算先用json记录下.

{% highlight json %} 

[
    {
        "title":"How Developers Stop Learning: Rise of the Expert Beginner",
        "link":"http://www.daedtech.com/how-developers-stop-learning-rise-of-the-expert-beginner",
        "summary":"",
        "category":"blog",
        "tag":["programming","Death sea effect", "Dunning–Kruger_effect"],
        "notes":"井底之蛙的一种, 停止学习的expert就不是expert了"
    },
    {
        "title":"Firebase",
        "link":"https://www.firebase.com/",
        "summary":"Scalable real-time backend Build apps fast without managing servers",
        "category":"service",
        "tag":["javascript","realtime","storage"],
        "notes":"cloud db, 不需要操心backend/server, js真是无所不能"
    },
    {
        "title":"Backlift Data persistence",
        "link":"http://backlift.github.io/docs/persistence.html",
        "summary":"In Backlift any app can store data on the server and retreive it later. This allows apps to implement complex functionality, such as collecting data from users via forms and visualizing that data in meaningful ways, or cordinating moves in a multiplayer game. You don't need to understand databases or SQL to store and retrieve data, just a basic understanding of javascript and jQuery. If you know how to fetch data jusing jQuery's ajax() methods, you can use the Backlift persistence API.",
        "category":"wiki",
        "tag":["javascript","backbone.js","backlift"],
        "notes":""
    },
    {
        "title":"ALTWWDC",
        "link":"http://altwwdc.com/",
        "summary":" free and open alternative to Apple's Worldwide Developer Conference - June 10th-14th, 2013. Five days of talks, food, co-working, and mingling with other developers all without the bar noise. Got a WWDC ticket? Didn't get a WWDC ticket? Doesn't matter - the conference happens outside the conference.",
        "category":"conference",
        "tag":["WWDC"],
        "notes":"WWDC一票难求, 退而求其次?"
    },
    {
        "title":"PQL",
        "link":"https://github.com/alonho/pql",
        "summary":"PQL stands for Python-Query-Language. PQL translates python expressions to MongoDB queries.PQL uses the builtin python ast module for parsing and analysis of python expressions.PQL is resilient to code injections as it doesn't evaluate the code.",
        "category":"library",
        "tag":["python","mongodb"],
        "notes":"pythonic way"
    },
    {
        "title":"Falcon",
        "link":"http://falconframework.org/",
        "summary":"The high-performance cloud API framework",
        "category":"library",
        "tag":["python","web","api","framework"],
        "notes":"叫Falcon的项目还真多"
    },
    {
        "title":"Porting Python 2 Code to Python 3",
        "link":"http://docs.python.org/dev/howto/pyporting.html",
        "summary":"With Python 3 being the future of Python while Python 2 is still in active use, it is good to have your project available for both major releases of Python. This guide is meant to help you choose which strategy works best for your project to support both Python 2 & 3 along with how to execute that strategy.",
        "category":"wiki",
        "tag":["python","python3","portable"],
        "notes":""
    },
    {
        "title":"Sleep: Everything You Need To Know",
        "link":"https://medium.com/the-healthy-life",
        "summary":"1. Set Up A Sleep Schedule 2. Quiet, Dark and Cool 3. Relaxation 4. Track It.",
        "category":"life",
        "tag":["sleep"],
        "notes":""
    },
    {
        "title":"ReactiveCocoa",
        "link":"https://github.com/ReactiveCocoa/ReactiveCocoa",
        "summary":"ReactiveCocoa (RAC) is an Objective-C framework for Functional Reactive Programming. It provides APIs for composing and transforming streams of values.",
        "category":"library",
        "tag":["FRP","Cocoa","Objective-C"],
        "notes":"Cocoa FRP framework"
    },
    {
        "title":"函数式反应型编程(FRP) —— 实时互动应用开发的新思路",
        "link":"http://www.infoq.com/cn/articles/functional-reactive-programming",
        "summary":"描述系统中数据(消息)流的结构关系，至于环境变化如何导致某些数据流变化，这些变化了的数据流又如何导致其它的相关数据流变化，压根儿不需要关心。这是一种编程范式，称之为Reactive Programming。",
        "category":"blog",
        "tag":["FRP","javascript"],
        "notes":"基本概念解释的不错"
    }
]
{% endhighlight %}
