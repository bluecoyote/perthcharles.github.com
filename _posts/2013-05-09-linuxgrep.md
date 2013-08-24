---
layout: post
title: "linux命令学习(七)：grep高级用法与正则表达式初步+sed+awk"
description: ""
category:shell 
tags: 
---
{% include JB/setup %}

##grep 高级用法  
	#grep -An -Bm -n -v  [--color=auto] '搜索字符串' filename
	-An	输出找到行之后的n行
	-Bm	输出找到行之前的m行
	//复习之前的用法
	-n	附带输出相应行号
	-v 	反向选择
	-i 	忽视大小写

	//为了让找到的字符串自动加上颜色，修改~/.bashrc,添加如下命令
	alias grep='grep --color=auto'
	//使更改后的文件生效
	#source ~/.bashrc

***  
##关于正则表达式需要注意的点  
1.处理单元是行  
2.正则表达式的结果可能收到不同语系编码的影响  
3.如需查找具有特殊含义的符号，需要使用转义字符'\'  
###集合[]用法  
[]中可以包含多个字符，如[abcd]。含义为:出现abcd四个中的任意一个都可以，而且出现且仅出现一次。  
	#grep 't[ab]st' filename	//找出filename中所有的tast和tbst串
^反选符  
	#grep '[^g]oo' filename		//找出filename中所有包含'oo'字符串且'oo'前面不是字符g的出现
-连续出现  
	#grep '[a-z]oo' filename	//找出filename中所有以a到z的字符开始后接oo的出现
	#grep '[[:lower:]]' filename	//效果与上句类似，但是排除了语系不同可能带来的干扰
###行首与行尾字符^$  
行首字符'^',这点要与集合[]中出现的^区别开  
	#grep -n 'the' filename		//找出filename中所有以the开始的行
	#grep -n '\.$' filename		//找出filename中所有以'.'结束的行
	#grep -n '^$' filename		//找出空白行

###任意一个字符和重复字符(. 和 *)  
'.'表示有且仅有一个字符  
'*'表示重复0个或多个前面的字符，这点与通配符(表示任意个字符)'*'需要区分开  
	#echo o |grep 'oo*'	//如果按照通配符的理解，至少需要两个oo后接任意个字符,但实际上这条命令的含义是找到至少含有一个o，且后面跟0个o或多个o的所有字符串
	//下面命令的含义是：找到字符串开头和结尾都是g，且两个g之间只能存在字符o，且至少有一个
	#grep -n '^goo*g$' filename

###sed命令用法  
	#sed [-nefi] [action]
	-n	仅输出经过特殊处理的那些行到屏幕
	-e	直接在命令行模式下进行sed动作的编辑
	-f	直接将sed的动作写在一个文件内 -f filename
	-i	直接修改读取的文件内容，而不是由屏幕输出
###sed命令很强大，也很繁琐。所以这里不罗嗦直接上我练习的几个命令  
	#nl /etc/passwd | sed  '2a drink tea' |sed '4a drink tea, too' |grep -A3 -B3 'drink tea'			//在第2行和第4行添加相应内容
	#nl /etc/passwd | sed  '2a drink tea' |sed '4a drink tea, too' |sed -n '2,5p' |grep -A3 -B3 'drink tea'		//在上一条的基础上只显示2-5行数据
	#nl /etc/passwd | sed  '2a drink tea' |sed '4a drink tea, too' |sed 's/drink/drinking/g' |grep -A3 -B3 'drink.* tea'	//将drink替换为drinking
	#ifconfig eth0 |grep 'inet addr' |sed 's/^.*addr://g' |sed 's/Bcast.*$//g'	//用两次替换，将电脑的IP地址从ifconfig中抽取出来
	#ifconfig eth0 |grep '9' |sed 's/^.*addr://g' |sed 's/Bcast.*$//g' |sed '/^.*X.*$/d'	//删除特定的行，显示IP地址
	#ifconfig eth0 |grep '9' |sed 's/^.*addr://g' |sed 's/Bcast.*$//g' |sed 's/^.*X.*$//g' |sed '/^$/d'		//将某些特定的行替换为空行，并删除
####将一行变多行  
首先通过将不要的字符替换成空格或直接删除，随后将分割符替换为换行符\n即可  
	#cat tmp | sed 's/^\[//g'|sed 's/\]$//g'|sed 's/,/\n/g'|sed 's/ //g'
###awk命令  
awk对比sed：awk主要针对行内数据进行操作，sed主要是以行为单位进行操作  
命令语法格式：  
	#awk '条件类型1{动作1} 条件类型2{动作2} ...' filename
awk过于复杂，所以以后慢慢练习。  
####awk 计算方差  
	#awk '{a[++i]=$1;} END{for(i in a)sum += a[i];ave=sum/NR;for(i in a) delta += (a[i]-ave)*(a[i]-ave);print delta/NR}' tmp
###其他好用命令：  
diff+patch:  
	diff用来比较两个文件的差别(虽然我基本都用vimdiff)，如果结合patch命令还能完成版本管理的一部分功能呢。命令如下：
	#last > last.text	//生成一个文件
	#cat last.text | sed '3,5d' |sed '$d' > last.text2	//生成一个*更新*的文件
	#diff -Naur last.text last.text2 > last.patch		//比较两个文件
	#ll last.text*	
	-rw-rw-r--. 1 zhongbin zhongbin 29298 May 21 15:28 last.text
	-rw-rw-r--. 1 zhongbin zhongbin 29030 May 21 15:30 last.text2
	#patch -p0 < last.patch //更新，将旧文件按照diff的结果更新到新的文件
	#ll last.text*
	-rw-rw-r--. 1 zhongbin zhongbin 29030 May 21 15:33 last.text
	-rw-rw-r--. 1 zhongbin zhongbin 29030 May 21 15:30 last.text2
	
