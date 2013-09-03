---
layout: post
title: "从文本中抽取出指定的行"
description: ""
category: shell
tags: []
---
{% include JB/setup %}

###问题描述  
给定文本a(上千行),按照文本b中指定的行号抽取出对应内容。  
需要保证文本b的行号是有序的。  
*需要学习awk命令*   
	#cat a
	adsf
	dgfegd
	f
	hh
	ee
	ee
	fhhh
	qqq
	uu
	#cat b
	1
	3
	4
	7
	#awk 'NR==FNR{a[FNR]=$0;next}($0 in a){print a[$0]}' a b >c
	#cat c
	adsf
	f
	hh
	fhhh

###可能遇到问题  
测试awk版本为3.1.7 
如果文本b不是顶格写的，则会无法得到正确的输出！*这点待解决*   
如果碰到只会输出最后一行的数据，请试着检查文本格式，可以尝试  
	#dos2unix a b
###参考资料  
[怎么样对文本进行指定行的数据提取操作？](http://bbs.chinaunix.net/thread-3605498-1-1.html)  

