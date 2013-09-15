---
layout: post
title: "[python学习笔记之二]常用模块和方法"
description: ""
category: python
tags: []
---
{% include JB/setup %}

###模块加载方法  
1.generic imports  
语法：import [module]  
这种方式称之为generic import.在使用模块中的函数时，需要加上模块的前缀  
如下例：  
	import math
	print math.sqrt(25)

2.function imports  
语法：form [module] import function  
这种方式教适合仅需要使用到模块的一个函数的情形，且使用函数时无需加模块前缀  
如下例：  
	from math import sqrt
	print sqrt(25)

3.universal imports  
语法： from [module] import *  
这种方式类似使用通配符，将模块中所有的函数和变量都导入了  


###获取模块中可用的方法  
需要知道某个模块中都有哪些能用的方法，可以使用下面的方法得到  
	import math
	print dir(math)


###python build-in method  
1.字符串处理的方法：在[python 基本入门](http://perthcharles.github.io/python/2013/09/04/python-learing-1)中有介绍  

2.数值比较函数：max,min,abs  

3.变量类型检查：type()  
	>>>print type(4)
	<type, 'int'>
	>>>type(4) == int
	True





###常用模块  
1.math：常用数学函数  
2.matplotlib: 画图模块，与matlab函数接口类似  


