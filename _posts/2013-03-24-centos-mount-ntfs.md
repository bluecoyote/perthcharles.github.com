---
layout: post
title: "在centos系统下，挂在ntfs格式的磁盘分区"
description: ""
category: centos6.4
tags: centos mount
---
{% include JB/setup %}

###前提介绍  
在我在WIN7系统下硬盘安装好双系统后，有不少时候需要访问一些WIN7系统下的文件，如果反复的重启电脑的话那就太烦人了。而Centos又不能直接挂载ntfs格式的磁盘分区，网上搜来一圈找到一个可行的方法  

###需要的软件  
*fuse*  
	#rpm -qa |grep fuse //查看系统是否已经安装软件  
	#yum list |grep fuse  
	#yum install fuse  
如果你的源里面没有这个软件，那就去添加更好的源吧，不会添加源的可以参照我另一片博客：[yum使用指南](http://perthcharles.github.com/centos6.4/2013/03/18/yum-using)  

*ntfs-3g*  
这个软件我选择的从源码安装，当然你也可以选择从yum源安装  
[ntfs-3g下载地址:www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/)  
	#./configure && make && make install  

###挂在分区  
在安装好上面这两个软件后，应该就可以挂在ntfs磁盘分区了  
	#fdisk -l //查看硬盘所有分区  
	#mount -t ntfs-3g /dev/xxx /mnt/xxx  
如果想开机就挂在上的话，我的方法是修改/etc/profile，再最后加上上面的mount命令  

