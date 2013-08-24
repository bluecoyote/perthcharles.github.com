---
layout: post
title: linux系统信息+文件编码格式转换
description: ""
category: linux-learning
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
