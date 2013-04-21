---
layout: post
title: "linux命令学习（四）"
description: "读文件操作命令：cat tac + more/less 权限与命令之间关系"
category: 
tags: shell
---
{% include JB/setup %}

###常用命令简介  
cat:从第一行开始显示文件  
tac:从最后一行开始显示文件  
nl:显示的时候顺便显示行数  
more:一页一页地显示文件内容  
less：与more类似，但是支持向上翻页  
head:只看头几行  
tail:只看结尾几行  
od:以二进制的方式读取文件内容（效果不太好，希望以后找到合适的工具）  

###一些更细节的解释  
cat:是concatenate(连续)的简写  
tail:如果想检测一个持续被写入的文件，可以输入下面的命令  
	#cat -f filename  
**-f**的含义是follow，是指將新增加(append)到文件的内容打印出来  

***
###用户能进入某个目录  
让用户能够进入某个目录成为“可工作目录”的基本权限需求：  
	可使用的命令：例如cd等切换工作目录的命令  
	目录所需权限：用户对这个目录至少需要有x权限  
	额外需求：如果用户想要在这个目录内利用ls查阅文件名，则用户对此目录还要有r的权限  
###用户在某目录下读文件  
用户在某个目录内读取一个文件的基本权限需求：  
	可使用的命令：例如cat,more,less等  
	目录所需权限：用户对这个目录至少需要有x权限  
	文件所选权限：用户对文件至少需要具有r的权限才行  
###用户修改文件  
用户修改一个文件的基本权限需求：  
	可使用的命令：vim等  
	目录所需权限：用户在该文件所在的目录至少需要x权限  
	文件所需权限：用户对该文件至少要有r,w权限  
####其他注意  
让一个用户可以创建一个文件的基本权限要求是用户在该目录要有w,x的权限  
让用户进入某目录并执行该目录下的某个命令的基本权限要求是用户对目录和对应文件都至少要有x的权限  