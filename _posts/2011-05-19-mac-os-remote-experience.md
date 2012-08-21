---
author: hewig
title: Mac OS X远程体验
excerpt:
layout: post
category:
  - iOS
tags:
  - mac os x
  - vnc
post_format: [ ]
---
在V2ex偶然发现了苹果派的[免费os X远程体验环境即将推出，开放预约][1]这个帖子，就预约了，其实我主要是想看下pppoe在mac底下命令行是如何配置的。算起来当年也和小唐子折腾过一阵子黑苹果，在家的台式机也装过10.4.7，后来装显卡驱动挂掉了，再后来就是在虚拟机上和苹果体验店。还没有远程体验过mac。这个环境配置用的是vnc，我最早是在用rhel的时候用过，不过现在都是直接ssh了。

我使用的客户端是开源的tightvnc，注意选择High-speed network，见下图，这是最省事的方法，这个选项主要是为了打开全屏，否则连上后屏幕会一闪而过。

[![image][3]][3]

输入用户名密码，登录。

[![image][4]][4]

可以看到，安装的是10.5.2，CPU是AMD的，这和在intel x86机器上装mac没什么区别，皓龙支持的指令集就包括x86。

[![image][5]][5]

现在对OS的没什么特别的要求，因为很多服务都可以通过浏览器来搞定，10.5.2自带的是safari 3，传说中的safari reader mode好像在5.0版本才支持。

[![image][6]][6]

也不支持mac app store，snow leopard才支持。

[![image][7]][7]

dashboard，widget平铺的效果很华丽；dock就不用说了吧

[![image][8]][8]

似乎默认没有装pppoe或者pon，由于没有权限本来想使用下安装和使用下macports或者homebrew的，终端感觉没有gnome-terminal或者konsole好用。。

[![image][9]][9]

Application目录下有不少应用程序，其中Textmate被誉为mac下最好用的编辑器之一。

[![image][10]][10]

不过windows底下有替代品~

[![image][11]][11]

自带了ruby,python,java等环境，再mac底下写code应该蛮爽的

[![image][12]][12]

体验到这一步就结束了吧，远程连上去有点卡，像播放slide一样，而且mac的不仅仅是mac os x而已，因为苹果现在仍然是软硬都做，mac机器细节部分做的很好，总而言之，mac os x还是值得尝试的。

再次感谢Michael Won和提供的体验环境~

[![][13]  
][13]  

 [1]: http://www.a-pie.com/2011/04/%E5%85%8D%E8%B4%B9os-x%E8%BF%9C%E7%A8%8B%E4%BD%93%E9%AA%8C%E7%8E%AF%E5%A2%83%E5%8D%B3%E5%B0%86%E6%8E%A8%E5%87%BA%EF%BC%8C%E5%BC%80%E6%94%BE%E9%A2%84%E7%BA%A6/
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image2.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image3.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image4.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image5.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image6.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image7.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image8.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image9.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image10.png
 []: http://kernelpanic.im/blog/wp-content/uploads/2011/05/image11.png
 []: javascript: