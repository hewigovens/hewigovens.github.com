---
layout: post
title: "关于Package Uninstaller"
description: ""
category: 
tags: ["mac", "OSX", "package", "uninstaller"]
---
{% include JB/setup %}

###2013/12/18 Update

Apple的EvenBetterAuthorizationSample的例子(非Sandbox)用NSXPCConnection和SMJobBless, 效果一样, NSXPCConnection相当于xpc的Cocoa接口, 不过10.8之后才能用.

###End

在Mac下你肯定有过这种体验: 通过Installer安装的有些App并没有提供卸载工具; 简单的从/Applications移除在MAS安装的App其实会残留很多文件.

Pacakge Uninstaller旨在提供一种通用的方法来卸载由Installer安装的App(下文将简写成PU), 特别是那些没有提供卸载工具的App. 代码托管在[这里](https://github.com/hewigovens/PackageUninstaller), 下载放在[这里](https://github.com/hewigovens/PackageUninstaller/wiki).

PU目前只是个Proof-of-Concept, 还不支持卸载像MS Office或者Cisco WebEx这类不是很标准的装法的程序: 先安装到临时目录, 然后在postinstall脚本里移动到目的地. 另外安装过程中通过脚本创建的文件也不支持. 如果要做到这些, 可能就需要hook Apple Installer了.

这里要吐槽下Office, 简直有滥用pkg文件的嫌疑, 安装的时候就是100+的pkg, 每次升级又是几百个, 如果你真想彻底删除, 建议参考微软提供的这个KB
[How to completely remove Office for Mac 2011](http://support.microsoft.com/kb/2398768). 祝你好运, :)

PU本来是想做像Windows控制面板那样, 是System Preferences的一个面板, 但是Apple的`AuthorizationExecuteWithPrivileges`的替代API`SMJobBless`似乎只从main bundle里去找helper? 所以最后改成了独立的App.

PU的原理也蛮简单的, 如果你熟悉Apple的Installer的话, 你肯定知道Installer或者storeagent(MAS的App实际上是通过它安装的)安装完pkg后会在`/var/db/receipts/`下生成一份receipt, receipt里记录了安装的路径,权限,大小等信息. PU会去遍历并过滤所有的receipts; 真正删除的动作是交给后台的helper去做的.

后台的helper是一个以root权限运行的xpc service, 虽然xpc service的设计目的并不想让人这么用, 但是据我观察, Github的Mac客户端也是这么干的, SourceTree的Mac客户端做法略有不同, 可能是自己用domain socket实现的IPC或者是直接用的`launch_msg`. 我这么怀疑是因为helper里也用到了`launch_msg`, 作用是卸载的时候尝试移除同名的launchd job. 不管怎么说, 看来比起命令行传参数或者执行某个脚本, 大家觉得还是IPC比较优雅.

PU的最开始是考虑用DO的, 除去传统Unix的一些IPC方法, 用的多的就是DO了. 这篇文章值得一读[The Good and Bad of Distributed Objects](http://www.mikeash.com/pyblog/friday-qa-2009-02-20-the-good-and-bad-of-distributed-objects.html), 这里主要提一下DO不好的地方, 我是因为第3条才不用的:

1. 对基本类型没什么支持, 需要实现NSCoding的对象才可以. 
2. 对于error handle支持不太符合OC的通常做法, 连接断掉DO会抛出异常, 而大部分OC的代码对异常支持不太友好. 我们之前遇到过这个坑, 解法是加上try/catch. 
3. 安全问题, 默认DO没有加密, 也没有比较好的机制来保证安全性. 还有就是因为OC的特性, 可以很容易用class-dump来看出你的方法名. 这里可以看看[Apple是怎么隐藏新feature](https://github.com/JaviSoto/iOS7-Runtime-Headers/commit/6ccf9c4526992fec0dc414d48e4a3f7446e9822f)的: 开发过程中先把方法命名成这种外人猜不到的`isYoMamaWearsCombatBootsSupported`, 然后在GM的时候改回正式命名. 不过这种最后时刻改方法名真的大丈夫?

helper里还有一个trick是用`stat /dev/console`来判断当前的登录用户, 然后通过`getpwuid`来取得用户的home路径, 后来发现这种做法可能会有问题, 因为用户的HOME环境变量可能会和getpwuid的结果不一致, 可以考虑通过IPC作为参数传过来.

helper在卸载的时候会尝试搜索用户的Caches/Containers/Preferences路径, 如果有bundle id相同的文件或文件夹也会删掉. 根据我自己的测试, 基本效果还不错, MAS下的App基本无压力, 我司带kext, TP-Link带kext的App也能删掉. 不过也有误伤的情况, 比如你装了一个SIMBL的插件, 然后删除的时候会把整个SIMBL的文件夹也给删掉, 因为SIMBL不在PU自带的白名单里. 以后改成让用户确认下删除的列表会比较保险.

--End