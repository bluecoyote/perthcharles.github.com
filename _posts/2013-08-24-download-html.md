---
layout: post
title: "wget 下载单个网页后，解析出包含的链接后，再下载"
description: ""
category: 
tags: 
---
{% include JB/setup %}

###下载单个网页并解析  
使用wget下载一个网页之后，在linux环境下对其解析出包含的所有链接，之后再将这些链接对应的文件下载  
	#wget [url]
	#cat test.html |sed 's/</\n/g' |sed 's/>/\n/g' |grep 'href="http' \
	|cut -f 2 -d ' ' |sed 's/"/\n/g' |grep http > urls.txt
	#cat urls.txt |xargs -n 1 wget

