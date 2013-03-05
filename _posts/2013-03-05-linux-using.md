---
layout: post
title: "linux命令学习（二）"
description: ""
category: 
tags: shell
---
{% include JB/setup %}


###本地帮助文件  
一般系统安装（yum、spt-get、手动）软件后，都会有一些帮助你使用或理解的文件，除了REAMME之外，还可以查看一个路径获得有更多信息。  
	#cd /usr/share/doc/  
### whatis = man -f  
	#whatis date  
	date (1)             - print or set the system date and time  
	#mam -f date  
	date (1)             - print or set the system date and time  
	更多请查看：  
	#man man  
###关机前检查  
	#who      //查看现在都有谁在线  
	#netstat  //查看网络的联机状态  
	#ps -aux  //查看后台程序  
	#reboot   //重启电脑  
	#shutdown -h now //立即关机  
	#shutdown -r now //立即重启  
	#shutdown -h 10  //10分钟后关机  
	#poweroff	        //断电关机  
	#init 0          //执行等级设置为关机  

