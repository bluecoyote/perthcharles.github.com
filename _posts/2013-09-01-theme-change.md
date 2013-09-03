---
layout: post
title: "github博客主题the-program的修改"
description: ""
category: 
tags: git
---
{% include JB/setup %}

默认的主题有的时间一长，就会多少感觉出一些不足之处。尤其是看到其他博主的博客主页搭建的更加的专业，不免有自己动手去改动主题的想法。主要参考了[风雨钝剑](http://realasking.github.io/)的[这篇](http://realasking.github.io/%E7%BD%91%E7%BB%9C%E5%86%B2%E6%B5%AA/2013/07/15/makeblog2/)博客。  

###改动_includes/themes/the-program/下的default.html文件  

1.将导航栏的多余滑动条删除  
在列表中仅仅保留：logo,crchive,page,category和tag即可。我是觉得那个滑动条有点多余，大家可以根据自己喜好修改。  

2.加入google站内搜索  
具体的加入方法请看[我的这篇博客及其参考资料](http://perthcharles.github.io/2013/03/08/test-search/)  
现在直接在default.html中加入如下代码即可：  
	<div class="misc vcard">
		<!--Google站内搜索开始-->
		<form method=get action="http://www.google.com/search" target="_blank">
		<input type=text name=q>
		<input type=submit name=btnG value="搜索">
		<input type=hidden name=ie value=utf-8>
		<input type=hidden name=oe value=utf-8>
		<input type=hidden name=hl value=zh-CN>
		<input type=hidden name=domains value="perthcharles.github.io">
		<input type=hidden name=sitesearch value="perthcharles.github.io">
		</form>
		<!--Google站内搜索结束-->
	</div><!-- misc vcard -->

3.右侧导航栏加入文章分类和最近发的博客列表  
直接上代码吧，稍微了解一点html相关的知识应该就能看懂。  
	<div class="misc vcard">
		<h4>Categories</h4>
  		<ul class="tab_box">
  		{% assign categories_list = site.categories %}
  		{% include JB/categories_list %}
		</ul>
  	</div><!-- misc vcard -->
	<div class="misc vcard">
  		<h4>Recent posts</h4>
  		<ul>
  		{% for post in site.posts limit:10 %}
  		<li class="post_title"><a href="{{post.url}}">{{post.title}}</a></li>
  		{% endfor %}
  		</ul>
  	</div><!-- misc vcard -->
4.其他更多的方法，请直接查看[风雨钝剑的这篇博客](http://realasking.github.io/%E7%BD%91%E7%BB%9C%E5%86%B2%E6%B5%AA/2013/07/15/makeblog2/)  

###总结一下：  
	其实主要的就是更改theme当中的default.html文件。所以更加直接的方式就是：如果发现有牛人的博客的主页上面有你比较喜欢的特性，你可以去github上找到他的repo，之后对照看default.html有哪些修改即可。直接看代码才是王道。  

