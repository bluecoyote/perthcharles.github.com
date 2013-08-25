---
layout: post
title: "获取虚拟机被自动分配的IP地址"
description: ""
category: KVM
tags: []
---
{% include JB/setup %}

##问题背景  
使用virt-install方式安装并管理虚拟机是一种很方便的手段。省去了我们许多对于网络的配置工作，唯一的缺点就是无法直接获取虚拟机的IP地址。很多时候需要手动进入虚拟机后查看或更改，略显得麻烦。而网络上能找到的诸多方法都需要比较麻烦的配置（个人感受）。直到找到[这篇博客](http://rwmj.wordpress.com/2010/10/26/tip-find-the-ip-address-of-a-virtual-machine/)，才感觉找到了我想要的方法。  
但是[这篇博客](http://rwmj.wordpress.com/2010/10/26/tip-find-the-ip-address-of-a-virtual-machine/)有一点不完整。就是对于一个新建的虚拟机，还没有使用网络登录上去时，是无法通过arp获取MAC与IP地址直接映射关系的。  
最终通过使用virsh+kvm+vnc+arp的组合方法，实现了完全校本化的获取虚拟机被自动分配的IP地址的方法。  

##脚本内容与解释  
我喜欢直接在代码中进行解释，如果想知道每个步骤更详细的原因可以查看后面的参考文献。  

1.[这篇博客](http://rwmj.wordpress.com/2010/10/26/tip-find-the-ip-address-of-a-virtual-machine/)中的方法  
	#根据虚拟机名称或编号得到配置信息
	virsh dumpxml vm-name
	#得到vm的mac地址
	virsh dumpxml vm-name|grep 'mac address'| cut -c 21-37
	#由于通过rdesktop连接会走网络，可以通过arp获得mac地址与IP地址的对应关系
	arp -an |grep `virsh dumpxml vm-name|grep 'mac address'| cut -c 21-37`
	#对上面命令的输出做点文本处理就可以得到IP地址
	output-from-up | sed 's/(/\n/g' |sed 's/)/\n/g' |grep 192

2.主要解决arp无法获取新建VM的地址映射关系  
	#virsh list  //显示当前安装好的虚拟机
	#virsh vncdisplay vm-name   //根据vm-name获取用于VNC连接的port-id
	#vncviewer port-id	//通过vncviewer连上虚拟机，至此arp就能获取地址映射关系，从而找出虚拟机的IP地址（可能延时会比较大）


###下面这个工具对我不work!
上述方法有个缺点就是arp可能需要经过较长时间才能获取到需要的信息，进一步调研发现有这么一个工具：[virt-ifconfig](http://git.et.redhat.com/?p=virt-tools.git;a=summary)。安装步骤如下：  
	#从仓库中获取一个snapshot
	#解压缩后执行autogen.sh
	#执行configure发现机器少了一些perl模块
	#添加epel源才是最终解决方法！添加后直接yum安装即可。

###最终的解决方法  
实践告诉我，还是[serverfault](http://serverfault.com/)这类专业的问答网站的答案靠谱！  
使用virt-install新建的虚拟机的IP地址和MAC地址对应关系在下面的文件中：  
	/var/lib/misc/dnsmasq.leases
直接读取这个文件即可！  

	
##参考资料  
[Tip: Find the IP address of a virtual machine](http://rwmj.wordpress.com/2010/10/26/tip-find-the-ip-address-of-a-virtual-machine/)  
[libvirt vnc console without virt-manager](http://blog.rot13.org/2012/12/libvirt-vnc-console-without-virt-manager.html)  
[Get list of DHCP clients with KVM+libvirt](http://serverfault.com/questions/101982/get-list-of-dhcp-clients-with-kvmlibvirt)  
