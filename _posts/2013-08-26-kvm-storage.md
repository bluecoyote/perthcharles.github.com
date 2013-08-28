---
layout: post
title: "KVM虚拟机镜像(disk img)的共享--尝试"
description: ""
category: KVM
tags: []
---
{% include JB/setup %}

##共享disk文件  
virt-install disk选项中有关于disk权限的参数：perms  
默认值为：rw(read/write),还有ro(readonly)和sh(shared read/write)。  
所以可以尝试从一个img启动多个虚拟机，但可能每个虚拟机都要有私有的根文件系统的img。  
下面是[Using shared storage with virtual disk images](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Virtualization/sect-Virtualization-Shared_storage_and_virtualization-Using_iSCSI_for_storing_virtual_disk_images.html)中的一些解释：  
	The virt-install command can be used to install new guests from the command line. The --disk argument can take the name of a storage pool, followed by the name of any contained volumes. Continuing this example, the following command will begin the installation of a guest with two disks; the first disk is the root file system, the second disk can be shared between multiple guests for common data:
	# virt-install --accelerate --name rhelx86_64 --ram 800 --vnc --disk \ vol=kvmguest/10.0.0.1 --disk vol=kvmguest/10.0.0.2,perms=sh --pxe
	The second disk has the <shareable/> flag set. Critical for the disk to be safely shared between guests, this ensures that the SELinux labelling will be appropriate for multiple guests to access the disk and that all I/O caching is disabled on the host.

##我的设想：
首先尝试sh启动多个虚拟机，不行则尝试尝试ro+sh启动一个，然后多个虚拟机  
最后实践发现将img的perms=sh的VMs可以依次起来，但是毕竟共享的是系统盘，终究还是会出现系统方面的错误，所以不推荐。  

##perms=sh的用途  
最后可行的方式就是只共享一些纯数据盘，这样只要操作得当，基本不会出现问题。  


