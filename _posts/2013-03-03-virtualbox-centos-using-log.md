---
layout: post
title: 虚拟机CentOS使用记录-安装篇
description: ""
category: linux-learning
tags: CentOS6.3
---
{% include JB/setup %}


###Install CentOS in VirtualBox  
	Centos 6.3 LiveCD  
	share dir:CentOS-Shared  
	install openssh in Centos  
###Shutdown the firewall  
	#service iptables status  //查看防火墙状态  
	#service iptables stop/start  //关闭或开启防火墙  
###安装并开启ssh服务  
	#yum install openssh  
	#service sshd status  
	#service sshd start/stop  
###设置host ssh to guest失败  
	VirtualBox version:4.1.12-1  
	ubuntu(host):12.04LTS  
	CentOS(guset):6.3  



