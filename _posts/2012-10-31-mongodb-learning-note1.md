---
layout: post
title: "MongoDB学习笔记(1)"
description: ""
category: 
- nosql
tags:
- mongodb
---
{% include JB/setup %}

记录一下学习10genM101 MongoDB for Developers的笔记。 
 
* MongoDB是非关系型的数据库，自我定位是高性能+足够多的feature。  
* MongoDB存储JSON Document，不同于传统数据库的表记录，而且JSON
* Document是schema less的，不同的JSON Document里的数据结构可以不同  
* MongoDB不支持SQL/Join/事务  
* Scale up，垂直扩展，即升级硬件，如CPU，内存，硬盘等。Scale out，水平扩展，即增加节点。MongoDB易于Scale out  
* MongoDB使用的默认端口是27017，db的位置/data/db，可以--dbpath指定，第一次启动的时候需要创建这个目录  
* mongo shell：
* - db.collection.find()/save().pretty()
* - 如果collection不存在会自动创建
* - 默认情况下MongoDB在存储JSON Document的时候会立刻返回，所以可能会fail quitely
*  mongodump/mongorestore是用来dump和restore db命令

我是直接`brew install mongodb`安装的，当然也可以直接下载安装。总的来说课程还不错，介绍了MongoDB的基本情况，并且是以实际的bottle+pymongo+mongodb来实现一个blog为主线来讲的，还介绍了一些bottle/python的基本知识。

唯一想吐槽的地方是，有些视频实际时间很短可以适当合并的。