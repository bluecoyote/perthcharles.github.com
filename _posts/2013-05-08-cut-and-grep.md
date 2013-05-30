---
layout: post
title: "linux命令学习(六)：cut grep && || sort wc uniq"
description: 
category: 
tags: Shell
---
{% include JB/setup %}

##命令执行时的判断依据  
在一行中执行多条命令可能用到的用法  
	//不管cmd1是否执行成功，都会执行cmd2. 就是依次执行cmd1和cmd2
	#cmd1;cmd2

	//若cmd1执行完成并正确执行，则开始执行cmd2；若执行出错则跳过cmd2
	#cmd1 && cmd2

	//若cmd1执行完成并正确执行，则跳过cmd2；若执行出错则执行cmd2
	#cmd1 || cmd2

***  
##选取命令：cut、grep  
###cut用法  
	#cut -d '分隔符' -f fields  <== 用于分隔字符
	#cut -c 字符范围            <== 用于处理排列整齐的信息
###cut参数解释  
	-d 后面跟分隔符，与-f一同使用
	-f 后面跟需要取出来的段号，从1开始计数
	-c 以字符为单位取出固定字符区间
###cut使用举例  
	//各段之间以'：'来分隔，命令取出第3和第5段
	#echo $PATH | cut -d ':' -f 3,5

	//用last在显示的登录者信息中仅留下用户名
	#last | cut -d ' ' -f 1

	//去掉export命令执行结果中每行的'declare -x '
	#export |cut -c 12-
###cut使用总结  
cut的主要用途是以行为单位进行数据分解，对有固定格式的行尤其有效  
***  
###grep用法  
	#grep [-acinv] [--color=auto] '待查找字符串' filename
	参数解释：
	-a 将binary文件以text文件的方式查找数据
	-c 计算找到符合条件的字符串的次数
	-i 忽略大小写
	-n 顺便输出行号
	-v 反向选择
	-r recursive递归的查找，用于文件夹中还有文件夹的情形
	--color=auto 可以将找到的关键字部分加上颜色显示
###grep举例  
	#last |grep 'root'
	#last |grep -v 'root'
	#last |grep 'root' |cut -d ' ' -f 1
	#grep 'MANPATH' /etc/man.config

	//在文件夹中找寻所有包含'include'的文件
	#grep -r 'include' *
***  
##sort参数  
	-f 忽视大小写
	-b 忽视每行最前面的空格
	-n 以纯数字进行排序
	-r 反向排序
	-u 相同数据仅出现一个代表
	-t 指定分隔符，默认为Tab
	-k 指定排序field
###举例  
	#cat /etc/passwd |sort
	#cat /etc/passwd |sort -t ':' -k 3
***  
uniq 和wc  
	#uniq [-ic]
	-i 忽视大小写
	-c 进行计数

	#wc [-lwm]
	-l 以行为单位
	-w 以单词为单位
	-m 以字符为单位
***  
更多文本处理命令tr col join paste expand split   
	#last |tr '[a-z]' '[A-Z]' 	//转换所有小写字母到大写
	#cat /etc/passwd |tr -d ':'	//删除输出信息中的':'
	
	#col -x 			//将tab扩展为空格

	#man col |col -b > /root/col.man	//将man文件转为文本文件方便查阅

	#paste -d ':' file1 file2		//将两个文件同一行粘帖在一起，如果file位置为'-',则表示输入来自standant input

	#expand [-t num] file			//将file的tab转为num数量的空格

	#split -b 300k file PREFIX		//将file文件切成大小为300k的文件组
	#ls -al |split -l 10 - lsroot		//将ls执行结果以10行为单位存成文件

	
