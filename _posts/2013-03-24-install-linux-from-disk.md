---
layout: post
title: "硬盘安装linux"
description: ""
category: 
tags: []
---
{% include JB/setup %}


###介绍  
目前正在用的系统是WIN7系统，由于现在系统性能表现越来越差，而自己又不想重新安装这个系统，所以就选择在电脑上面安装双系统。  
再者最近在学习linux，所以就干脆选择安一个linux来玩玩，目前选择的是CentOS6.4。至于为什么选择这个版本，大家都知道的：稳定！当然这样一来桌面软件支持就略显不足，不过暂时够用就好。  

###用到的软件  
EasyBCD:这款软件用来帮助你在WIN7系统下面制作启动项。这里只简单说明我用的步骤，更具体的使用方法请[google之](www.google.com)  
wingrub:利用这个软件，可以帮助你在制作EasyBCD启动项的时候确定你需要选用的分区号。  
Acronis Disk Director Suite:帮助你在WIN7下无损分区，目前用户体验良好。不过保险起见，最好还是先备份重要文件啦。  

###安装步骤  
话不多说，这就开工  
	打开EasyBCD->  
	Add New Entry->  //这一步就是给你liunx镜像文件制作启动项，或许在linux下更准确的说法是修改grub？  
	选择NeoGrub标签页->  
	点击Install,点击Configure,进行配置，其实我感觉这个是标准的grub的写法。最重要的是各个操作系统的配置文件对应镜像需要解压出来的文件有区别，这点很重要。很多人的博客并没有明显的区分或是主要针对Ubuntu这个系统进行讲解的    
最重要的就是配置了，这个地方网上有不少人进行了解释，但是我觉得我觉得最简单最实用的还是百度空间的[小治的空间](http://hi.baidu.com/sf_chipan),在此感谢作者！  

###各个系统的配置文件写法和镜像需要解压缩的文件  
####CentOS系列  
文件目录
	CentOS-xx-i386/x86_64-bin-DVD1/2.iso  
	initrd.img  //initrd.img和vmlinuz这两个文件在ioslinux文件夹下  
	vmlinuz  
	images/  
配置文件
	title install centos XXX  
	kernel (hd0,6)/vmlinuz  //hd0 表示你的镜像文件放在你电脑对应的那块硬盘；6表示镜像存放分区的编号。  
	initrd (hd0,6)/initrd.img  

####其他系列  
其他发行版本目前还没有尝试，有需求的话，可以去参考百度空间的[小治的空间](http://hi.baidu.com/sf_chipan)  


####几点注意事项  
***  
配置文件中对应的分区编号可以用wingrub帮忙确定的^_^  
***  
镜像文件最好放在linux能够识别的文件系统中，由于FAT32单个文件最大不能超过4G，对于CentOS-DVD安装可能就不能可行了。大家可以尝试放到ext系列的文件系统下(推荐ext3)  
***  
再多说一句，如果你想在WIN7环境下识别ext3文件系统的分区的话，可以安装Ext2Fsd这个软件。  
***  
