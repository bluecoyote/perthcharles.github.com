---
layout: post
title: "linux常用工具列表"
description: ""
category: linux-learning
tags: tools
---
{% include JB/setup %}

###常用工具列表  
*git*  
	#git add *
	#git commmit -a -m "commit-name"
	#git push origin master
	#git clone XXX
xsel:命令行复制到剪切板  
	#cat filename |xsel -b -i  
goagent：不懂的自己查去  
	#python proxy.py  
iconv:解决打开windows txt文件中乱码问题  
	#iconv -f gbk -t utf8 from.txt > to.txt
screen:实现在断开ssh的情况下，在服务器上继续执行程序  
	#screen -S screen-name	//新建一个sreen
	#ctrl+a+d		//先按ctrl+a,然后再按d即可保留screen，下次ssh连接服务器后可以重新进入这个screen
	#exit			//如果在某个screen里面的工作完成后，该命令可以完全退出screen
	#screen -ls		//查看目前在跑的screen
	#screen -r screen-name or id	//恢复screen
foxit reader  
	#wget http://cdn04.foxitsoftware.com/pub/foxit/reader/desktop/linux/1.x/1.1/enu/FoxitReader-1.1-0.fc9.i386.rpm

