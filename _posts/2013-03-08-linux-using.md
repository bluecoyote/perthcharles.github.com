---
layout: post
title: "linux命令学习（三）"
description: ""
category: 
tags: shell
---
{% include JB/setup %}


###关于pwd  
	#cd /var/mail   
	#pwd	//显示当前完整路径  
	/var/mail  
	#pwd -P	//显示当前真实路径，而非使用链接的路径  
	/var/spool/mail  
	#ls -al  
	（前面略去...）/var/mail -> /var/spool/mail  
**注：**当一个文件夹是一个链接文件时，上述两个命令的执行结果会出现上例中的不同  

###创建多层目录  
	#mkdir test/test  
	mkdir: cannot create directory `test/test': No such file or directory  
	#mkdir -p test/test  
参数**-p**將帮助你把不存在的上层目录建立起来  
mkdir还有-m参数：手动配置文件属性，而不用默认值  
	关于属性：r=4,w=2,x=1,故7=4+2+1表示具有可读可写可执行的权限  


