---
layout: post
title: 初识Jekyll
category : 
tags : git
---  
{% include JB/setup %}  

##关于 Jekyll  
首先，Jekyll不是一个博客软件，更加准确的说法应该是一个解析器。当你按照Jekyll事先定义好的规则写好了一篇博客后，它会自动的將对应文件解析成最终的博客样式。  


##关于Page  
Pages支持较多文件类型，我主要用MARKDOWN和HTML这两种文件类型。任何根目录下和不是以下划线开始的子文件夹下的Page文件都能够被Jekyll自动解析。  

##关于Post  
新建一个post可以用下面的命令  
	#rake post title="name of post"  
这样产生的文件会在文件夹：_posts下，且后缀名为：**md**  
注意：后缀名不能为MARKUP，否则jekyll不能正确解析post文件

##新建page  
	#rake page name="name of page"


##Categories和Tags  
这两个功能只能针对post生效，对page没有作用。具体的用法是在post文件的最开始定义好这些内容。如这篇post对应的定义内容如下：  

	---
	layout: post
	title: 初识Jekyll
	category : tools
	tags : jekyll
	---  
这种定义形式叫做：YAML Front Matter，更多细节解释请查看[YAML Front Matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter)  


##关于themes  
现在用的主题名为：the program,安装方法为：  
	#rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"  
	#rake theme:switch name="the-program"  

##我的posts列表样例  
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



##参考资料  
[基于jekyll的github建站指南](http://jiyeqian.github.com/2012/07/host-your-pages-at-github-using-jekyll/)  
[Bootstrap官网](http://twitter.github.com/bootstrap/)  
[Liquid官网](http://liquidmarkup.org/)  
[使用Liquid模板语言](http://www.mceiba.com/develop/liquid-learn.html)  
[Zero to Hosted Jekyll Blog in 3 Minetes](http://jekyllbootstrap.com/)  
[像黑客一样写博客--Jekyll入门](http://www.soimort.org/posts/101/)  
[Markdown语法说明中文版](https://github.com/heiniuhaha/markdown-syntax-zhtw)  


