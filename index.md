---
layout: page
title: 博客简介
tagline: Supporting tagline
---
{% include JB/setup %}
##写该博客的初衷
读研之后，接触的东西日渐丰富。为了不被“淹死”，所以觉得非常有必要把自己每天学到的东西记录下来。试用了一些软件后发现很难满足自己各种无聊的要求，在特定的博客网站写又无法获得root权限，思来想去决定在github上面挂载自己的博客。边学边写，乐在其中。  

####脚踏实地，记录学习的点点滴滴  
####生命不止，奋斗不息  

## 主要内容  
  1.linux系统使用技巧  
  2.算法探讨  
  3.C/C++  
  4.计算机体系结构  
  5.操作系统  
  6.数据库  
  7.记录生命


##Post List  
<ul class="posts">
  {% for post in site.posts limit:5 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

###友情链接  
[潘海洋的博客](http://pocean.blog.163.com/blog/#m=0)  
[黎明灰烬的博客](http://www.jackwish.net/)  
[东大学子](http://blog.sina.com.cn/jiaoyou11)  

