---
layout: post
title: "linux 安装软件问题：XXX share library can not found"
description: ""
category: 
tags: []
---
{% include JB/setup %}

###问题  
当跑某些软件的时候，可能会遇到下面的错误：  
	"XXX share library" can not found
如果你可以确定这个库你已经安装好了，则可能是环境变量没有设置正确。主要环境变量就是LD_LIBRARY_PATH。  

###解决方法  
	#whereis XXX //如果库的文件名是libXXX.so
	#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/the-result-of-last-commond/lib/

如想免去开机重启后的重复设置，将上面的export语句写到.bashrc文件中即可。  

