---
layout: post
title: "linux命令学习(一):du xargs "
description: ""
category: shell
tags: 
---
{% include JB/setup %}


##查找软件安装位置方法  
	#whereis name-of-software  
##查看通过yum已安装的程序  
	#rpm -qa |grep 程序名  
##du读取文件大小  
	#man du  
	#du -h  //自动的用更易读的方法输出结果  
##xargs（好用）  
xargs能够將上一个命令的执行结果当作参数传递给下一个命令。忘记细节了，请记得：  
	#man xargs  
举例：將find找到的文件，传递给du命令  
	#find /etc -name *id.conf |xargs du -h  
##删除文件夹内全部文件  
	#rm -f *  //-f意味着不一一提示是否删除  
**注**：当文件夹没文件过多或文件名长度过长，会导致*argument list too long*的错误，我理解的原因就是正则式“*”展开导致命令行长度过长。这是UNIX以来就有的限制。查看限制可使用命令：  
	#getconf ARG_MAX  //我的电脑是2097152  
删除所有文件：执行ls得到文件夹所有文件的路径，xargs將ls的输出，每10个一组（以空格为分割符）作为rm -rf 的参数  
	#ls |xargs -n 10 rm -rf  
删除符合特定命名的文件,其实多少个一组是可选的:  
	#find -name XXX |xargs [-n 10] rm -rf  
