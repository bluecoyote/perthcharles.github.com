---
layout: post
title: "git multi user error"
description: ""
category: 
tags: git
---
{% include JB/setup %}


##如果在同一台机器上尝试使用多个git帐号，可能遇到下面这个问题：  
	#git push origin master
	ERROR: Permission to repo1.git denied to user2.		//repo1.git 属于user1.所以出错点已经很明显。
	fatal: The remote end hung up unexpectedly
	#ssh git@github.com -v	//检测github识别的用户
	Hi user2! You've successfully authenticated, but GitHub does not provide shell access.	//看到了吧，github识别的是第二个帐号
上面这种问题出现的情况可能是你的ssh key配置出现问题，尝试各种选择，最终适合我的解决方法是：  
*删除user2中的ssh key*，因为我的问题是同一个key加到了两个不同的帐号里面，这样可能github不支持，而只认识最早加上这个key的用户。  


##参考资料  
[Getting Started - First-Time Git Setup](http://git-scm.com/book/en/Getting-Started-First-Time-Git-Setup)  
[Git's famous “ERROR: Permission to .git denied to user”](http://stackoverflow.com/questions/5335197/gits-famous-error-permission-to-git-denied-to-user)  


