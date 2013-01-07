---
layout: post
title: "MongoDB学习笔记(Final)"
description: ""
tags:
- mongodb
- mmoc
- nosql
---
{% include JB/setup %}

---

为期7周的M101 MongoDB for Developers上周结束了, 成绩也出来了:

<img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/images/m101_final_score.png" width=640>

Question 7是选错答案了, 因为我只看了计算出来的一串数字的首尾几个数字, 然后就选了; 另外一题则是漏选了~

算起来, 这是我第一个完整的上完的在线课程，这和一定要完整的从头到尾的读完一本书一样，值得纪念一下~

在线的课程应该是未来的趋势，[MOOC](http://en.wikipedia.org/wiki/Massive_open_online_course)这样的术语也应运而生, 这能一定程度解决天朝教育资源分配不均的问题, 比如有些学校的计算机教育实在是落后. 

补上之前的笔记:

##Week4 Performance

这周主要是介绍Performance, 主要讲了索引. MongoDB为了保持key有序使用的是B树. 建立正确的索引能显著提高读的性能, 写由于需要更新index反而会变慢.

使用的一些例子:

{% highlight js %}
db.students.ensureIndex({
    student_id: 1,
    class: -1
}, {
    unique: true,
    dropDups: true,
    sparse: true,
    background: true
})
//创建索引
//unique参数, 保证index中的key是唯一的
//dropDups参数, 移除重复的key, 行为是随机的
//sparse参数, only contain entries for documents that have the indexed 
//field. Any document that is missing the field is not indexed. 

db.foo.ensureIndex({a:1, b:1})
//multikey index(key:[array])
//invalid:db.foo.insert({a:[1,2,3], b:[5,6,7]})

db.places.ensureIndex({location:'2d',type:1})
db.places.find({location:{$near:[74,140]}}).limit(3)
//geo index~

db.system.indexes.find()
//查看当前db的所有索引
db.students.getIndexes()
//查看studens集合的索引
db.students.dropIndex({student_id:1})
//删除索引

db.students.stats()
db.students.tootalIndexSize()
//索引的大小, not free

db.students.find({}).hint()
//suggest mongodb use which index
//In pymongon, the parameters of hint() is a list of tuples.

db.system.profile.find()
db.system.profile.find({millis:{$gt:1000}}).sort({ts:-1})
mongdod --profile 1 --slowms 100

db.setProfileingLevel(1,100)
db.getProfilingLevel()
//Useful for performance tuning


//Some Comments:

//Use dot notation for embeded part
//Index creation is in forground by default, 
//It's faster but mayblock other writers
//A background index creation still blocks the mongo shell that 
//you are using to create the index.Although the database server 
//will continue to take requests, 
//A mongod instance can only build one background index at a time 
//per database.
//$gt/$lt/$ne/$existes/$regex not efficient in using index

//index cardinality

//regular  : 1:1
//sparse   : <= collection documents
//multikey : >> collection documents


{% endhighlight %}

###Explain command

具体每项的解释可以看这里:[http://docs.mongodb.org/manual/reference/explain/](http://docs.mongodb.org/manual/reference/explain/)

{% highlight js %}

db.zips.find({"_id":"35004"}).explain()
{
	"cursor" : "BtreeCursor _id_", // use index, if BasicCursor, not use index
	"isMultiKey" : false,
	"n" : 1,			// return documents
	"nscannedObjects" : 1,
	"nscanned" : 1,
	"nscannedObjectsAllPlans" : 1,
	"nscannedAllPlans" : 1,
	"scanAndOrder" : false,
	"indexOnly" : false,
	"nYields" : 0,
	"nChunkSkips" : 0,
	"millis" : 0,		// query time, a slow query > build in 100ms
	"indexBounds" : {
		"start" : {
			"_id" : "35004"
		},
		"end" : {
			"_id" : "35004"
		}
	},
	"server" : "freyr.lan:27017"
}

{% endhighlight %}


##Week5 Aggregation

这周主要介绍了Aggregation框架, 与传统SQL对比可以看
[SQL mapping chart](http://docs.mongodb.org/manual/reference/sql-aggregation-comparison/)

	
###Pipeline concept 


Aggregation的基本理念基本和Unix的管道类似, 链式的一系列操作:

	$project -> $match -> $group -> $sort -> $skip -> $limit -> $unwind (unjoin data)
	1:1      -> n:1    ->    n:1 ->   1:1 ->   n:1 ->    n:1 -> n:1

使用的一些例子:

{% highlight js %}

db.products.aggregate([{
    $group: {
        _id: "$category",
        "num_products": {
            $sum: 1
        }
    }
}])
//A little like upsert, iterate all documents, return new collections

{_id:{"manufacture":"$manufacture",category:"$category"}}
//group by multiple key:
//compound id
//_id can be document, must unique 


db.zips.aggregate([{
    $group: {
        _id: "$state",
        population: {
            $sum: "$pop"
        }
    }
}])
//计算每个state的总人口数

db.zips.aggregate([{
    $group: {
        _id: "$state",
        postal_codes: {
            $addToSet: "$_id"
        }
    }
}])
//统计每个state的所有邮编

db.zips.aggregate([{
    $project: {
        _id: 0,
        city: {
            $toLower: "$city"
        },
        pop: "$pop",
        state: "$state",
        zip: "$_id"
    }
}])
//or
db.zips.aggregate([{
    $project: {
        _id: 0,
        city: {
            $toLower: "$city"
        },
        pop: 1,
        state: 1,
        zip: "$_id"
    }
}])
//Reshape~

db.zips.aggregate([{$match:{pop:{$gt:100000}}}])
//人口大于100000的state

db.zips.aggregate([{$sort:{state:1,city:1}}])
//排序

{% endhighlight %}

###Limitations:

1. 16MB document
2. 10% of the memory on a machine
3. sharding, mongos
4. mapreduce/hadoop


##Week6 Application Engineering

这周主要探讨了如下几个话题:

1. Durability of writes
2. Avalibility fault tolerance
3. Scaling

###Write concern

通常在mongodb的driver可以配置, 如pymongo. 值得一提的是课程还没结束pymongo就release新版本了[pymongo 2.4](http://api.mongodb.org/python/current/)~

	Warning DEPRECATED: Please use mongo_client instead.


{% highlight py %}

import pymongo
m = pymongo.MongoClient()
print m.write_concern
# {}
m.write_concern = {'w': 2, 'wtimeout': 1000}
print m.write_concern
# {'wtimeout': 1000, 'w': 2}
m.write_concern['j'] = True
print m.write_concern
# {'wtimeout': 1000, 'j': True, 'w': 2}
m.write_concern = {'j': True}
print m.write_concern
# {'j': True}
m.write_concern['w'] = 0
#Disable write acknowledgement and write concern

# SafeMode == {'w': 1,'j':False}
# w=n: write ack back from n nodes
# j: journal, complete inserted to db
# w='majority'

# wtimeout=1000
# if mongod nodes is 3, 'w' is 4 and not set wtimeout
# wait tcp timeout maybe more than 10 mintues


{% endhighlight %}

###Possiable Network errors


1. The network TCP network connection between the application and the server was reset between the time of the write and the time of the getLastError call.
2. The MongoDB server terminates between the write and the getLastError call.
3. The network fails between the time of the write and the time of the getLastError call



###Replication

At least 3 mongod nodes, If primary is down, secondary will elect new primary. It's transparently for client. If primary is up after down.(Failover and Rollback or copy data from currently primary).

Both primary and secondary can read, But only primary can write.

Replication sync between primary and secnodary is asynchronous:

	secondary query primary's oplog.rs collection acoording to timestamp.
	type `show collections` in mongo shell can see more details

###Replicate set nodes type:

1. regular 
2. arbiter
3. delayed -> can not become primary 
4. hidden  -> never primary


####Create:

{% highlight bash %}

mongod --replSet rs1 --logpath "1.log" --dbpath ~/data/rs1 --port 27017 --fork --shardsvr/--configsvr
mongo --port xxxx

{% endhighlight %}

####Config:

{% highlight js %}

config = {}
rs.initiate(config)
rs.status()
rs.slaveOk()
//can read from secondary now

rs.isMaster()
rs.conf()
rs.help()

{% endhighlight %}


####Client

`pymongo.MongoReplicaSetClient`

###Sharding

Need a config server(another mongod instance)

Sharding implications:

	1. every documents contains the shard key
	2. shard key is immutable
	3. Should index the shard key
	4. shard key update must set parameter `multi`
	5. Query without shard key -> query all shards
	6. no unqiue key unless / begin or part of shard key

-END-
