---
layout: post
title: "vim 编码相关问题"
description: ""
category: linux
tags: vim
---
{% include JB/setup %}

###vim中文乱码问题--本机设置  
首先应该选用utf8格式的编码比较靠谱，同时为了防止乱码现象，应该保障系统设置和vim的设置相一致  
	#echo $LANG //查看系统当前选用编码方式  
	#LANG=zh_CN.utf8  
	#vim /etc/vimrc  //将set fileencodings 设置如下  
	set fileencodings=utf8,gbk,big5,ucs-bom,latin1  
###其他推荐的设置  
中文环境GBK码  
	#LANG=zn_CN.gbk  
	#vim /etc/vimrc  
	set fileencodings=gbk,big5,ucs-bom,latin1  
中文环境UTF8参照之前的本机设置  
英文环境就直接用就好了，所以推荐装机的时候就选择英文系统，毕竟码代码还是英文用的多点    

