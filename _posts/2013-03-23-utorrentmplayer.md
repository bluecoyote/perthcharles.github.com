---
layout: post
title: "utorrent+mplayer使用"
description: ""
category: 软件使用  
tags: 
---
{% include JB/setup %}


###utorrent  
为了在centos上面下载六维空间的资源，就必须选择一个给力的下载器，但是目前utorrent客户端只有WINDOWS版本，所以就必须曲线救国了。我的方法如下：  
首先确保你添加了第三方的源，如果不会添加请移步[yum 源的使用](http://perthcharles.github.com/centos6.4/2013/03/18/yum-using/)  
然后安装在linux环境下安装windows软件的平台，想了解更多的请[google wine](www.google.com)  
	#yum installl wine  
安装好wine环境后，只要下载一个windows环境下的utorrent.exe文件，就可以直接打开这个软件下载六维的软件了。开始享受吧！  

###mplayer使用  
	#yum list|grep mplayer  //查看你的源中是否有mplayer  
	#mplayer [-fs] filename  //-fs是可选项，表示全屏播放  
需要说明的是我的mplayer没有安装图形界面(自己懒的动)，所以只能选择在命令行下输入命令播放视频，不过够用就行。  


#### 无线网卡配置  
目前笔记本的无线网络功能处于无效状态。同时目前还没有需求，所以就没有配置。  
