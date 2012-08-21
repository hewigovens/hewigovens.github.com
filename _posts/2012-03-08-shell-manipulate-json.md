---
author: hewig
title: shell下操作json
excerpt:
layout: post
category:
  - Linux
tags:
  - bash
  - json
  - shell
post_format: [ ]
---
最近需要在shell下操作json，当然正常情况下直接python -c “import json ooxxx”就ok了。考虑到脚本会被部署到不同的客户环境下，python版本会有些差异，如Mac 10.5默认的python版本是2.5，10.6默认的是2.6，10.7默认的是2.7，而貌似json库是在2.6才引入的，2.5的话只能用simplejson之类的第三方库。  
索性搜索了一下，看有没有直接在shell下直接操作json文件的方法。

Json.org推荐了两个：[Jshon][1]和[JSON.sh][2]

其中JSON.sh是完全用shell实现的json parser，似乎不能做到添加/修改/删除原有json的结构。而jshon是用c实现的，依赖于jansson，使用MIT协议，目的就是为了替代由grep/sed/awk写的fragile adhoc parsers，相比之下python/perl/ruby显得过于笨重了。

至于使用，参照jshon的文档，拿个json文件试验一下就知道了，对shell很友好：从stdin读入，操作，输出到stdout，和其他的*nix文本处理命令结合使用也很容易。

下面说说我的使用场景，向json文件插入对象，然后必要的时候容易的插入的对象删除。比如：

    $ cat test2.json
    {
     "nbndkplefmmhmcmfjanjaakhhkiegogd": {
      "external_crx": "extension.crx",
      "external_version": "1.0"
     }
    }
    

插入对象的话，执行：

    $ ./jshon -n {} -i "key" -e "key" -s "value1" -i "key1" -s "value2" -i "key2" -p < test2.json
    

    {
     "nbndkplefmmhmcmfjanjaakhhkiegogd": {
      "external_crx": "extension.crx",
      "external_version": "1.0"
     },
     "key": {
      "key1": "value1",
      "key2": "value2"
     }
    }
    

-i是insert的意思，-n表示新建非string的对象，如object，-s表示是新建string，-e，extract，我理解为进入某一级，-p，则退回上一级；删除的话，会简单一点，指定key就好了，如

    $ ./jshon -d "nbndkplefmmhmcmfjanjaakhhkiegogd" < test2.json
    {}
    

由于jshon依赖于Jansson，如果能将jansson静态链接进jshon，只需要带一个文件就好了，方便一些；这在Linux下很容易做到  
只静态链接Jansson，其他的还是动态链接。如：

    gcc -o jshon jshon.o -Wl,-Bstatic -ljansson  -Wl,-Bdynamic
    

但在Mac底下就不太好做，apple提供的ld根本就不认识-Bstatic或者-Bdynamic这样的编译选项，没办法只好动态链接了，但是Mac底下的动态链接只会搜索特定的位置，如/usr/local/lib，只好使用otool和install\_name\_tool来修改之，让jshon从当前路径中搜索libjansson.4.dylib，具体可以参考霍叔的这篇[如何使用第三方的dylib][3]。

顺带提下，在64位机器下如果需要编译32位版本jshon的，需要在编译jansson的时候指定为i386. 即./configure -arch i386，编译jshon的时候也要给CFLAGS和LDFLAGS加上-m32 -arch i386的参数。

[![][5]  
][5]  

 [1]: http://kmkeen.com/jshon/
 [2]: https://github.com/dominictarr/JSON.sh
 [3]: http://blog.devep.net/virushuo/2009/07/01/xcodecocoadylib.html "如何使用第三方的dylib"
 []: javascript: