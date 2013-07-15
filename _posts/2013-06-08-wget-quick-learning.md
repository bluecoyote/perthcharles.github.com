---
layout: post
title: "wget quick learning"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##基本用法  
下载一个指定网页的文件，默认存储为index.html  
	#wget http://www.example.com/

下载ftp站点文件  
	#wget ftp://ftp.gnu.org/pub/gnu/wget/wget-latest.tar.gz	//下载wget latest source code
下载某个*网站*目录下的所有gif文件  
	#wget -e robots=off -r -l1 --no-parent -A.png http://static.fsf.org/dbd/
	//-e		执行‘.wgetrc’格式的命令，wgetrc格式参见/etc/wgetrc或~/.wgetrc
	//robots=off	不使用默认遵循robto exclusion standard的设置
	//-r -l1	r表示递归下载，l表示限制递归下载层数，尽量配套使用
	//--no-parent	递归时不要追溯到父目录
	//-A .png	匹配后缀名为png的文件
下载整个网站(慎用)  
	#wget -r -l 0 http://www.example.com
更多高级用法请查看参考资料。  


注：通配符只适用于ftp站点，如可以使用如下命令批量下载某ftp网站的gif文件  
	#wget ftp://example/*.gif


###参考资料  
[wget参数用法详解](http://www.ha97.com/153.html)  
[wiki: wget](http://en.wikipedia.org/wiki/Wget)  

