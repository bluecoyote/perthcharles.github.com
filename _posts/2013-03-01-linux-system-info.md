---
layout: post
title: linux系统信息+文件编码格式转换
description: ""
category: linux
tags: 
---
{% include JB/setup %}


#系统信息相关  
####查看系统发行版本号  
	#cat /etc/issue
	#lsb_release -a
	#cat /etc/redhat-release(针对redhat,Fedora)  
####查看内核版本等信息  
	#uname -a //a 表示 all  
更多信息：[查看LINUX发行版的名称及其版本号的命令](http://xiaozhen1900.blog.163.com/blog/static/17417325720115713351300/)  

####linux下文件编码格式转换方法  
推荐工具：enca  
安装方法ubuntu：
	#sudo apt-get install enca  
使用方法：
	#enca -L zh_CN file  //检查file的编码
	#enca -L zh_CN -x UTF-8 file //將file转换为UTF-8编码格式  

####查看服务器CPU相关信息  
逻辑：  
	1台服务器有：N个CPU
	1个CPU有：M个核
	1个核有：P个超线程
不同CPU上核之间通信开销比同一CPU核之间通信开销大，所以搞清楚核之间的关系十分重要。  
	//CPU信息主要来源
	#cat /proc/cpuinfo
	//物理CPU个数
	#cat /proc/cpuinfo |grep "physical id" |sort |uniq |wc -l
	//每个物理CPU中核的个数
	#cat /proc/cpuinfo |grep "cpu cores"|cut -f 2 -d ':'
	//是否为超线程
	//如果同一个物理CPU上的逻辑CPU具有相同的core id,则超线程是打开的
	#cat /proc/cpuinfo |grep -E '(processor|physical id|core id)'
	
	//同时也可以查看下面目录下的文件，具体含义看文件名体会
	#cd /sys/devices/system/cpu/cpu0/topology/
	#ls
	core_id  core_siblings  core_siblings_list  physical_package_id 
	thread_siblings  thread_siblings_list

