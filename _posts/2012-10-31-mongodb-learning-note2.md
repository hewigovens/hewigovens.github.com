---
layout: post
title: "MongoDB学习笔记(2)"
description: ""
category: 
- nosql
tags:
- mongodb
---
{% include JB/setup %}

Week2介绍的是MongoDB的CRUD，主要是mongo shell和pymongo的使用。

在MongoDB中，和CRUD基本对应的是：

* C -> Insert
* R -> Find
* U -> Update
* D -> Remove

总体来说，MongoDB的操作对程序员来说是非常友好的，以programming language APIs(object/function call)的方式操作DB。

实际和MongoDB server通信使用的是[Mongo Wire Protocol](http://www.mongodb.org/display/DOCS/Mongo+Wire+Protocol)：

	The Mongo Wire Protocol is a simple socket-based,
	request-response style protocol.
	Clients communicate with the database server through a 
	regular TCP/IP socket

简单来说就是将描述操作的JSON Object序列化成[BSON](http://bsonspec.org/)，通过socket扔给mongod解析并处理。

MongoDB内部实际使用的都是BSON，binary格式的JSON超集，而mongo shell实际上是个交互式的javascript解释器，你可以运行基本的js语句。

每个MongoDB存储的Document都有一个唯一标示的字段：_id ，如果你没有明确指定，MongoDB会自动给你生成一个，形如`"_id" : ObjectId("50906d7fa3c412bb040eb577")`

###Insert/Update的一些例子:
{% highlight js %}
* db.collection.insert({"name":"value"})
* //添加一个document，参数直接是json object
* db.collection.findOne()
* //随机返回一个document
* db.users.findOne({"username":"dwight"},{"email":true,"_id":false})
* //查找username为dwight的所有documents，只显示email字段
* db.collection.find()
* //只会返回20项，默认情况下server 10min后会关闭这个cursor
{% endhighlight %}

###Query operator一些例子：
{% highlight js %}
* //mongodb中的Query operator基本上是以embeded document的方式来处理的:
* db.grades.findOne({"student_id":{$gt:20}})
* //还有$gt $lte
* $exists
* //看字段是否存在
* $type
* //根据字段的类型来查找
* db.users.find({name:{$regex:"q"},email:{$exists:true}})
* //$regex 支持正则表达式，libpcre/perl
* $or:[{score:{"$lt:50"},{}]
* //逻辑or，特别之处是一个prefix operator，原因主要是为了符合json的格式
* db.scores.find( { score : { $gt : 50 }, score : { $lt : 60 } } );
* - //$and, 如果两个相同的key，起作用的是会是后一个key的值，这是个小陷阱

{% endhighlight %}

###多态查询:
{% highlight js %}
> db.movies.find()
{ "_id" : ObjectId("5098fa4d1d45e3ddd35f98a1"), "name" : "gone with the wind" }
{ "_id" : ObjectId("5098fa8a1d45e3ddd35f98a2"), "name" : [ "inception", "killer" ] }
{ "_id" : ObjectId("5098faa41d45e3ddd35f98a3"), "name" : "inception" }
> db.movies.find({'name':'inception'})
{ "_id" : ObjectId("5098fa8a1d45e3ddd35f98a2"), "name" : [ "inception", "killer" ] }
{ "_id" : ObjectId("5098faa41d45e3ddd35f98a3"), "name" : "inception" }
{% endhighlight %}

###Dot notation
如果要查询embeded document，MongoDB也提供了dot notation的方式，值得注意的是dot notaion必须用引号括起来才行。

###sort/skip/limit:

{% highlight js %}

* db.scores.find({"type":"exam"}).sort({score:-1}).skip(50).limit(20)
* //find()返回的是一个cursor, 可以进行排序，或者跳过，返回限定数目的结果，
* //这里值得注意的地方是，sort/skip/limit实际上都是在server上处理的
* 而且顺序一定是sort->skip->limit，真正执行query实际返回结果的时候
{% endhighlight %}

###Update/Remove/Drop
{% highlight js %}

* db.scores.update({…})
* //update默认的行为除了_id，替换成新的json document
* //如果需要删除某个key，可以使用$unset:{key:1}，修改可以使用$set/$inc:

* db.scores.update({score:{$lt:70}},{$inc:{score:20}},{multi:true})
* //给所有分数低于70的加上20, multi很重要  
* //默认update只会更新一个返回的结果，这个多半是随机的  
* //multi的意思是更新所有，实现上是cooperative的write/yeild.

* db.scores.remove()/drop() 
//drop比remove快很多，remove相当于批量update，drop则时直接删除数据结构
{% endhighlight %}


###Misc
{% highlight js %}

* db.runCommand({"getLastError":1})
* //error field 如果是空则表明命令执行成功了，否则会有出错信息
* db.scores.count()
* //计数
{% endhighlight %}

###pymongo
pymongo风格和python基本保持一致，这也可以算做对程序员友好~，比如：

* findOne()在python中就是find_one()
* 还有一些参数上的略微不同：比如cursor的sort()，参数是tuple的数组，原因是dict是无序的，这里也是个小陷阱。
* update()的第三个参数不是json object而是直接`multi=True upsert=True`
* 一些helper func：save()/find_and_modify()	
