---
layout: post
title: "MongoDB学习笔记(3)"
description: ""
category: 
tags:
- mongodb
---
{% include JB/setup %}

Week3主要介绍的是MongoDB的schema desgin。

在传统关系型数据库设计schmea的时候，经常会有规范化的要求：


	Three goals of normalization relational world?

	1. free the database of modification anomalies(一致性，eg,email)
	2. minimize redesign efforts
	3. avoid biasing any particular aceess parttern

我对这个没有太多的接触，体会不多，但是在MongoDB里，主要是application driven design：根据实际的data access pattern来设计，如访问数据的频率？读的多还是写的多？那部分数据经常更新？是否需要原子操作等。

MongoDB是Document Oriented，基本上也不需要什么ORM中间件了，一大优势~，不过MongoDB不支持常见的一些约束，如外键约束、事务等，这些就需要应用程序或者程序员来保证了。

总结起来MongoDB的schema design推荐的做法是尽量prejoin/embed数据，MongoDB支持multi key index（可以在mongo shell调用cursor的explain方法来查看是否启用了索引），所以对embeding支持的很好，读取的效率也很高。

那什么时候不建议embeding呢？主要有如下两个原因：

1. 超过16MB的Document
2. 减少working sets, 比如只想更新部分数据


###其他
{% highlight js %}
//表示树型结构
//Given the following typical document for a e-commerce
//category hierarchy collection called categories
{
  _id: 34,
  name : "Snorkeling",
  parent_id: 12,
  ancestors: [12, 35, 90]
}

db.categories.find({ancestors:34})

{% endhighlight %}

{% highlight python %}
#存储大文件
#store large files(>16MB)

import gridfs
{% endhighlight %}
