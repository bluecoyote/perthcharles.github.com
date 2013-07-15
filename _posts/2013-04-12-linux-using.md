---
layout: post
title: "linux 命令学习（五）：服务器登录消息 找含某字符串的所有文件"
description: ""
category: 
tags: shell
---
{% include JB/setup %}

##/etc/motd使用  
如果你正在使用一台服务器，并且想通知每一个新登录这台服务器的用户一个消息。  
比如你需要在服务器上进行一些测试工作，肯定希望其他登录进来的用户不要跑别的程序。这时你可以在/etc/motd文件中编辑你的通知消息，每一个新登录的用户都会看到这个消息。  
	#cat /etc/motd
	Hello everyone,
	This server will be used to run some test-programs at 2013/04/12 0:00 ~ 24:00
	Please do not login server at this time. ^_^

##找出含特定字符串的所有文件  
	#grep -ir (string-to-find) (search-files)

