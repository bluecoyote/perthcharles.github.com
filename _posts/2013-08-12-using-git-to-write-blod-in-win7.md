---
layout: post
title: "win7下搭建博客环境"
description: ""
category: 
tags: []
---
{% include JB/setup %}


##安装包下载地址  
[git for windows:msysgit](https://code.google.com/p/msysgit/downloads/list)  
[RubyInstallers](http://rubyinstaller.org/downloads/)  

##安装步骤  
1.依次安装msysgit和RubyInstaller,RubyInstallers需要仔细看下网页上的说明，下载对应的标准包和Dev包  
如rubyinstall-2.0.0-p247-x64对应DevKit-mingw64-64-4.7.2-20130224-1432-sfx.  
msysgit安装后的设置，请参考[初识git](http://perthcharles.github.io/2013/02/25/git-start)  

2.安装jekyll  
尝试一：在git bash中直接安装  
	问题一：gem:command not found  
	将ruby安装目录下的bin文件夹添加到系统路径中即可  
	#PATH=/c/Ruby200-x64/bin:$PATH  
	问题二：The fast-stemmer native gem requires installed build tools.  
	尝试一到此结束  
尝试二：双击Dev包解压后的msys.bat进行安装  
	解压路径必须是全英文的，否则脚本报错  
	执行命令：#gem install jekyll  
	时间可能会很长，但是能够执行成功。  
3.安装完成后，检测是否安装成功  
	#jekyll -version  
4.安装rdiscount  
	#gem install rdiscount --platform=ruby  
5.针对中文编码，修改ruby配置文件  
	Ruby 安装目录下的 lib\ruby\gems\1.9.1\gems\jekyll-0.11.2\lib\jekyll\convertible.rb 文件（找不到可以搜索，版本号可能会有不同），把  
	self.content = File.read(File.join(base, name))  
	替换成  
	self.content = File.read(File.join(base, name), :encoding => "utf-8")  
##参考资料  
[WINDOWS下安装jekyll并在本地预览](http://librajt.github.io/2012/09/08/using-jekyll/)  
[windows下安装DevKit](http://rubyer.me/blog/134/)  
[ ruby之——安装gem提示：Please update your PATH to include build tools or download the DevKit](http://blog.csdn.net/shandong_chu/article/details/7052478)  
[*这个博主写的博客不错*Jekyll 非你莫属](http://chxt6896.github.io/blog/2011/11/30/blog-jekyll-install.html)  
