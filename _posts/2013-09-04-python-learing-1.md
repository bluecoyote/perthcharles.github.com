---
layout: post
title: "[python学习笔记之一]基本入门"
description: ""
category: python
tags: []
---
{% include JB/setup %}

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



4.空格很重要  
缩进代码的时候，需要经常使用4个空格  

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
	count = count_no * 2 	//变量引用
	
