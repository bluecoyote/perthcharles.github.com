---
layout: post
title: "[python学习笔记之一]基本入门"
description: ""
category: python
tags: []
---
{% include JB/setup %}
###Why Python?  
在linux环境下工作的时候，使用shell脚本能够完成许多有趣的工作。  
在逐渐体会到脚本语言的强大后，日常工作中越来越离不开脚本语言了。  
每一种编程都有各自的局限性，所以shell bash也会有许多无法顺利完成的工作。  
在简单调查发现后，python作为一种解释型的语言，已经被广泛使用。  
同时还能完成更多独特的功能，比如matplitlib库支持许多matlab中类似的画图函数  
甚至还有matlab无法简单实现的功能，比如[这篇博客中画可变宽度的条形图](http://perthcharles.github.io/coding/2013/09/03/python-plot-bar/)  

说了这么多废话，该进入正题了。首先推荐我学习python的网站：[Codecademy](http://www.codecademy.com/)  
这个网站从之前学html的时候就有接触，主要需要都是偏前端开发方面的。  
还有一个很给力的功能值得推荐：[Codecademy Labs](http://labs.codecademy.com/#:workspace)  
这个功能给你提供了一个网络上的实践端口，实在是太给力了。  

其他在线手册：  
[Python Tutorial](http://www.tutorialspoint.com/python/index.htm)  


###基本入门  

1.输出  
	//打印字符串
	print "Welcome to Python"
	//打印浮点数，
	total = 54.634
	print("%.2f" %total) 	//结果为：54.63
	

2.变量声明  
有整形，浮点型,布尔型和string型，声明与使用方式跟shell类似  
string类型单独说明  
	my_int = 7
	my_float = 1.2
	my_bool = True	//python 是大小写敏感的语言
	my_int = 3  //对变量重新赋值

3.string类型  
能够像数组一样访问string类型的每个字符，同时自带许多有用的method  
	//声明时，单双引号都可以，但必须配套使用
	//字符串中对于单双引号需要使用转义字符'\'
	my_string1 = 'string1'
	my_string2 = "STRing2"
	//像数组一样使用string
	fifth_letter = "MONTY"[4]  	//计数从0开始，结果是fifth_letter = Y
	//获取字符串长度
	print len(my_string1)   	//结果为7
	//大小写转换字符串
	print my_string2.lower()	//结果为string2
	print my_string2.upper()	//结果为STRING2
	//类型转换
	pi = 3.14
	str(pi)		将浮点型转为字符型
	print "The value of pi is around:" + 3.14		//会报错
	print "The value of pi is around:" + str(3.14)	//正确执行
	//字符串拼接
	print "a" + "b" 	//结果为ab
	//关于打印string类型变量
	//语法： print "%s" % (string_variable)
	string_1 = "a"
	string_2 = "b"
	pirntf "%s is diff with %s." % (string_1, string_2)	//打印：a is diff with b.
	//检验字符串是否全是字母表中的字符
	string_1.isalpha()	//返回值是True 或 False
	//获取子串
	my_string1[0:2]	//获取[0,2)范围内的字符，结果为'st'
	my_string1[2:]	//获取[2,字符串末尾+1)范围内的字符，结果为'ring1'



4.空格很重要  
缩进代码的时候，需要经常使用4个空格  
python中基本上用空格代替了大括号的作用  

5.注释  
注释方法与shell类似，使用符号'#'进行注释  
	//注释单行
	#this is a comment
	//注释多行
	"""this
	is a multi-line
	comment"""

6.算数符号  
	count_no = 1 + 2
	conut_no = 5 - 2
	count_no = 2 * 10
	count_no = 20 / 4   	//整数除法，运算结果与C策略类似
	count_no = 5 % 3		//整数取模
	count_no = 2 ** 3 		//幂乘，结果为8
	count_no = 100 ** 0.5 	//相当于开方，结果为10.0
	count = count_no * 2 	//变量引用

7.显示当前时间  
	from datetime import datetime
	now = datetime.now()
	print now	//结果类似：   2013-09-14 13:58:00.377380
	pirnt now.month	//9
	print now.day 	//4
	print now.year 	//2013
	print now.hour	
	print now.minute	
	print now.second	

8.控制语句  
比较运算: == != < > <= >=  
含义与C中类似  

逻辑运算：and or not  
含义与C中&& || ! 类似  

if与elif,else  
	def greater_less_equal_5(answer):	//注意整个函数定义的缩进和冒号
		if (answer > 5):	//注意冒号
		    return 1
		elif (answer < 5):
			return -1
		else:
			return 0

	print greater_less_equal_5(4)
	
9.用户交互  
请求用户的输入：raw_input()  
	name = raw_input("What's your name?")

10.关于import  
import语句用于加载一个模块  
一个模块根本上就是一个定义了许多变量与函数的文件，与C中的头文件类似  
更详细的内容请查看[python 常用module](http://perthcharles.github.io/python/2013/09/14/python-learing-2/)  




###参考资料  
[Python v2.7.5 documentation](http://docs.python.org/2.7/)  
[Should I use Python 2 or Python 3 for my development activity?](Should I use Python 2 or Python 3 for my development activity?)  
[What’s New In Python 3.0](http://docs.python.org/3/whatsnew/3.0.html)  
[Python v3.3.2 documentation](http://docs.python.org/3/)  
