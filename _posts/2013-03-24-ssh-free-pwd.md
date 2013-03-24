---
layout: post
title: "ssh免密码登录"
description: ""
category: 
tags: ssh
---
{% include JB/setup %}

###博客背景    
有时候在两台服务器上面工作，需要同时操作它们，如果在两个窗口里面反复切换就显得很麻烦。所以先配置ssh免密码登录，然后用其他工具  

假设A是本地主机，B是远程主机。想要从A远程访问B的时候免密码登录  
首先在A上生成公钥和私钥，然后在B机器上记录在公钥    
	#(A)ssh-keygen -t rsa //连续三次回车，这里选择不设置密码  
	#(A)ssh root@ip-of-B  //这次还需要密码  
	#(B)ls -a  //查看是否存在.ssh文件夹  
	#(B)mkdir .ssh && chmod 0700.ssh && exit   
	#(A)scp ~/.ssh/id_rsa.pub root@ip-of-B:.ssh/id_rsa.pub //还需要输入密码  
	#(B)touch /root/.ssh/authorized_keys  //生成一个空文件，如果文件已经存在，则跳过这条命令  
	#chmod 600 ~/.ssh/authorized_keys  //设置该文件只有root能查看，因为这个文件是用于保存ssh客户端生成的公钥的，该文件是在ssh服务端配置文件/etc/sshd_config中指定的  
	#cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys  //将A传过来的公钥写入authorized_keys文件，注意这里必须使用 ">>"  

至此配置完成了，现在在A上面使用ssh登录B应该就不用输入密码了。  
###其他说明  
如果在A上面需要在脚本里面执行B机器上面的命令，除来使用实验室提供的工具外，可以简单的使用下面的方法  
	#ssh root@ip-of-B:/pwd "command1;command list"  
当然这里只是一个简单的例子，所以生成的密钥没有设置密码。如果是短期使用可以先这样配置使用，然后再将密码从B机器上面的authorized_keys里面删除，下次你再需要用的时候再将其加进去。这样安全性要好些，如果长期使用还是建议不要使用没有密码的密钥，特别是共用服务器。  

