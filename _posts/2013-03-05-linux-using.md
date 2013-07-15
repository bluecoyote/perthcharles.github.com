---
layout: post
title: "linux命令学习（二:关机 常见目录含义"
description: ""
category: 
tags: shell
---
{% include JB/setup %}


###本地帮助文件  
一般系统安装（yum、spt-get、手动）软件后，都会有一些帮助你使用或理解的文件，除了REAMME之外，还可以查看一个路径获得有更多信息。  
	#cd /usr/share/doc/  
### whatis = man -f  
	#whatis date  
	date (1)             - print or set the system date and time  
	#mam -f date  
	date (1)             - print or set the system date and time  
	更多请查看：  
	#man man  
###关机前检查  
	#who      //查看现在都有谁在线  
	#netstat  //查看网络的联机状态  
	#ps -aux  //查看后台程序  
	#reboot   //重启电脑  
	#shutdown -h now //立即关机  
	#shutdown -r now //立即重启  
	#shutdown -h 10  //10分钟后关机  
	#poweroff	        //断电关机  
	#init 0          //执行等级设置为关机  
###linux常见目录及其含义  
	#/  
		根目录(root)  
	#/usr  
		软件存放位置(Unix Software Resource)  
	#/etc  
		配置文件  
	#/opt  
		第三方软件  
		更多的情况是会装到**/usr/local/**目录下  
	#/boot  
		开机与内核文件  
		主要包括：Linux内核文件以及开机菜单和开机所需配置文件等  
		linux kernel常用的文件名为vmlinuz  
	#/boot/grub  
		如果使用grub引导装载程序，会存在这个文件夹  
	#/var  
		与系统运作过程有关  
	#/bin  
		放置的是在单用户模式下**还**能够被操作的命令  
		主要有cat chmod chown date mv mkdir cp bash等常用命令   
	#/dev  
		任何设备与接口设备都是以文件的形式存在于这个目录之中  
	#/lib  
		放置开机时会用到的函数库  
		**/lib/modules**会放置内核相关的模块(驱动程序)  
	#/media  
		放置可删除的设备  
	#/mnt  
		如需临时挂载设备，建议挂载到这个目录下面  

	#/sbin(system binary)  
		放置包括开机，修复，还原系统所需的命令。常见的有：fdisk,fsck,ifconfig,init,mkfs  
	#/usr/sbin  	服务器软件程序  
	#/usr/local/sbin  	自行安装的软件  
	
	#/srv(service)  
		常见的有网络服务WWW，FTP  
	
	#/lost+found  
		当文件系统发生错误时 ，將一些丢弃的片段放置到这个目录下  
		目录通常会在分区的最顶层  
	#/proc  
		其实是虚拟文件系统，放置的内容都在内存中，不占用实际的硬盘空间  
	#/sys  	与/proc文件夹类似  



