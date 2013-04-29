---
layout: post
title: "chrome bugs"
description: ""
category: 
tags: 
---
{% include JB/setup %}

###chrome bug  
不知到怎么回事，我本子(centos6.4)chrome每次打开后自动进入全屏模式，而且无法退出。尝试了一下方法：  
	#yum update google-chrome-stable.x86_64  //首先当然是想更新,结果无效
	//然后yum remove后再yum install，依然无效
	//最后找到可能原因是chrome配置出现了问题，所以先备份了先前的配置文件，然后重新让chrome生成一遍全新的配置文件
	#cd /.config
	#cp -r google-chrome google-chrome-bak 
	#rm -rf google-chrome
	//之后重新启动chrome，就像是chrome刚装上一样。
目前就是这样解决的无法退出全屏的问题，如果有更好的解决办法，请在博客下方留言，谢谢:)  

