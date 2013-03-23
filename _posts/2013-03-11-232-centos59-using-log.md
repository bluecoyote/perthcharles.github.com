---
layout: post
title: "centos5.9使用记录"
description: ""
category: 
tags: CentOS-5.9 服务器232
---
{% include JB/setup %}


###配置内网  
更改文件：/etc/sysconfig/network-scripts/ifcfg-eth0  
1,将dhcp改为static  
2,添加IPADDR，NETMASK，GATEWAY，DNS等字段  
###配置外网连接  
更改文件：/etc/resolv.conf,加入nameserver配置，然后重启网络服务  
	#service network restart  
