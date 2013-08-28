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
	--disk path=/path-to-img/test.img,size=20 \
	#使用光驱方法安装的镜像路径
	--cdrom /path-to-original-iso/xp.iso \
	--import
	#额外说明#若test.img存在，使用import+disk组合;若test.img不存在，使用disk+cdrom组合
	#额外说明#如果test.img不存在，则从xp.iso中安装并存储到test.img中；若test.img存在，则直接读取test.img内容安装系统。
	#启用KVM内核加速功能
	--accelerate \
	--vnc \
	--keymap=en-us

##virsh管理方法  
新安装好的虚拟机默认处于运行状态  
查看当前VM的状态  
	#virsh list --all
获取指定VM的domain id  
	#virsh list --all |grep running |cut -d ' ' -f 3   #这个地方-f 是3有点不太清楚，跑出来的结果就是要3 :(
	#virsh domid domain-name  //通过domain-name获取id
启动未在running状态的VM  
	#virsh list --all |grep -v running |cut -d ' ' -f 3 |xargs -n 1 virsh start
关闭指定VM  
	#virsh shutdown [domain-id, domain-name, ...]
	#virsh destroy [domain-id, domain-name, ...]  //强制关闭VM
删除一个VM  
	#virsh undefine domain-name
重启指定VM  
	#virsh reboot [domain-id, domain-name, ...]
挂起与恢复VM  
	#virsh suspend [domain-id, domain-name, ...]
	#virsh resume [domain-id, domain-name, ...]
根据domain id获取MAC地址，当然也可以根据VM名称  
	#virsh dumpxml domain-id |grep 'mac address' |cut -c 21-37
获取libvirt默认网络配置下VM的IP与MAC地址的对应关系  
	#cat /var/lib/misc/dnsmasq.leases
修改分配给VM的内存大小  
	#virsh setmem [domain-id or domain-name] count	//单位KB，新count不能超过创建VM时指定的大小
使用virsh管理虚拟网络  
	#virsh net-list
	#virsh net-dumpxml NetworkName	//查看特定网络的详细信息

##参考资料  
[KVM setup on debian squeeze](http://wiki.kartbuilding.net/index.php/KVM_Setup_on_Debian_Squeeze)  
[详细参数介绍](http://blog.csdn.net/starshine/article/details/6998189)  

