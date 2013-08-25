---
layout: post
title: "使用virt-install搭建KVM虚拟机"
description: ""
category: KVM
tags: []
---
{% include JB/setup %}

##virt-install安装脚本  
	virt-install \
	#虚拟机名字
	--name test \
	#客户端虚拟机的名称
	--ram 2048 \
	#指定虚拟机的虚拟CPU数
	--vcpus=1 \
	#检查指定的虚拟CPU数不要超过物理CPU数
	--check-cpu \
	#指定虚拟机能够使用的物理CPU
	--cpuset=0,2,4,6  or --cpuset=1-3,5,7-9
	#指定存储配置，path指定img的存放路径，
	--disk= path=/path-to-img/test.img,size=20 \
	#使用光驱方法安装的镜像路径
	--cdrom /path-to-original-iso/xp.iso \
	#若test.img存在，使用import+disk组合;若test.img不存在，使用disk+cdrom组合
	#额外说明#如果test.img不存在，则从xp.iso中安装并存储到test.img中；若test.img存在，则直接读取test.img内容安装系统。
	#--import
	#启用KVM内核加速功能
	--accelerate \
	--vnc \
	--keymap=en-us


##参考资料  
[KVM setup on debian squeeze](http://wiki.kartbuilding.net/index.php/KVM_Setup_on_Debian_Squeeze)  
[详细参数介绍](http://blog.csdn.net/starshine/article/details/6998189)  

