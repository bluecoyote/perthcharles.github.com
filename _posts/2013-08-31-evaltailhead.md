---
layout: post
title: "linux命令学习（八）:eval,tail,head,seq"
description: ""
category: shell
tags: []
---
{% include JB/setup %}

##eval  
查看系统自带的解释：
	#eval [arg ...]
		The  args  are read and concatenated together into a single command.  This command is then read and executed by the shell,  and its  exit status is returned as the value of eval.  If there are no args, or only null arguments, eval returns 0.
可以看出eval给shell提供了一种"根据变量的值，运行时确定所执行命令"的机制。  
实践过程中遇到的一种情况就是"包含变量的变量名的赋值"操作。如下面这段代码：  
	//用一个for循环，给名称为test_1,test_2等变量赋值
	#cat val_in_val.sh
	#!/bin/bash
	array=(11 22 33)
	for i in $(seq 3)
	do
		//使用eval 将${i}和$((i-1))先求出来
		//再真正执行下面的命令
		//test_1=${array[0]}   (i=0时)
		eval test_${i}=${array[$((i-1))]}
		//下面命令原理类似。其中'\'的作用是在eval执行时，
		//直接保留'$'符号而不作为求值符号处理
		//执行eval后，脚本中执行的相当于
		//echo "test_1=$test_1" (i=0时)
		eval echo "test_${i}=\$test_${i}"
	done
	#sh val_in_val.sh
	test_1=11
	test_2=22
	test_3=33


###head  
用于输出文件的起始的部分数据  
	#head -n 2 file  	//输出file文件的前两行
	#head -n -2 file	//显示除最后2行之外的其他行
	#head -c 2 file		//显示文件的头两个byte
	#head -c -2 file	//显示除最后两个byte之外的所有内容

###tail  
基本用法与head类似，但是也有更多高级的用法，详细内容请查看man tail  
单纯就输出而言，没有'-'符号的作用，而是'+'符号的应用。注意与head区分开。  
	#tail -n 2 file		//输出file文件的最后2行
	#tail -n +2 file	//输出文件除其实2行之外的内容
	#tail -c 2 file		//输出file文件的最后2个byte
	#tail -c +2 file	//输出file文件除起始2字节之外的内容

###seq  
打印一连串的数字，命令比较简单，直接上实例  
	#seq 4
	1
	2
	3
	4
	#seq -s '#' 3 6		//替换默认的分隔符\n为'#'
	3#4#5#6
	#seq -f s%3g -s ' ' 3 0.5 4 //以步长0.5，按指定格式输出
	s  3 s3.5 s  4
	#seq -f %f -s ' ' 3 0.5 4 //浮点格式输出
	3.000000 3.500000 4.00000
	#seq -s '' 10 |sed 's/[0-9]/*/g'	//输出11个*
	***********

