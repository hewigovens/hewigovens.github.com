---
layout: post
title: "hack电信HG8245"
description: ""
category: 
tags: ["hack", "telecom"]
---
{% include JB/setup %}

迁移宽带的时候发现光猫换成了华为的HG8425, 搜索了下"HG8425 破解"发现相当容易, 这样就可以省下一个路由器了.

查看HG8425的背面, 上面有默认的WiFI SSID和密码, WiFi连上后直接用root/admin telnet上, 找到telecomadmin的密码.

```
hewig@192.168.1.3 ➜  /Users/hewig
% telnet 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'.

Welcome Visiting Huawei Home Gateway
Copyright by Huawei Technologies Co., Ltd.

Login:root
Password:*****
WAP>shell

BusyBox v1.4.1 (2011-07-29 10:25:20 HKT) Built-in shell (ash)
Enter 'help' for a list of built-in commands.

WAP(Dopra Linux) # uname -a
Linux EchoLife_WAP 2.6.21.7-hrt1 #4 Sat Apr 14 16:36:05 HKT 2012 armv6l unknown
WAP(Dopra Linux) # cd /mnt/
/mnt/jffs2/   /mnt/nfs/     /mnt/usb1_1/
WAP(Dopra Linux) # cd /mnt/jffs2/
WAP(Dopra Linux) # ls
InformFlag            hw_boardinfo.xml      hw_spec.xml
customizepara.txt     hw_boardinfo.xml.bak  hwontlog.txt
custunpara.txt        hw_bootcfg.xml        main_version
cwmp_rebootsave       hw_ctree.xml          ontstatusfile
eponroguestatus       hw_ctree_bak.xml      watchdogInfo
fsok                  hw_default_ctree.xml
WAP(Dopra Linux) # grep telecomadmin hw_ctree.xml
<X_HW_WebUserInfoInstance InstanceID="2" UserName="telecomadmin" Password="XXXXXXXX" UserLevel="0" Enable="1"/>
WAP(Dopra Linux) # exit

success!
```

在网络->宽带设置里把原来连接类型为桥接的删掉, 再创建连接类型为路由的连接, 填上你的账号密码点应用就OK了.

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/hw8245_network_settings_zps575cb968.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/hw8245_network_settings_zps575cb968.png" border="0" alt=" photo hw8245_network_settings_zps575cb968.png" width=100%/></a>

<a href="http://s750.photobucket.com/user/hewigovens/media/Freyr/Blog/hw8245_network_settings2_zps6022b285.png.html" target="_blank"><img src="http://i750.photobucket.com/albums/xx144/hewigovens/Freyr/Blog/hw8245_network_settings2_zps6022b285.png" border="0" alt=" photo hw8245_network_settings2_zps6022b285.png" width=100%/></a>