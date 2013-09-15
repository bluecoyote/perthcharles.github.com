---
layout: post
title: "[python学习比较之三]lists 和 dictionaries"
description: ""
category: python
tags: []
---
{% include JB/setup %}

###List  
声明一个list: list_name = [item1, item2]  
中括号对应list  
与C中的数据较类似，但也具有重大区别：list的长度是可变的！  
	//给list添加新元素
	list_name.append(item)
	//获取list的长度
	len(list_name)
	//取部分list，类似对字符串的操作
	my_list = [0, 1, 2, 3]
	my_slice = my_list[1:3]	//结果是my_slice = [1, 2]
1.查找list中的item  
	a = [1, 2, 3, 4, 5]
	four_index = a.index(4)
	print four_index	//4对应的index为3
2.添加item至list  
	a = [1, 3, 4]
	a.insert(1, 2)	//在index为1的位置插入数值2
	print a 	//[1, 2, 3, 4]
3.使用for循环对list进行操作  
语法：  
	for variable in list_name:
		#do stuff
语法上跟shell的类似，但是格式上需要注意*冒号*的使用  
	
4.对list进行排序  
使用list_name.sort()会对list进行排序，排序原则是：按数字或字母增序排列  

5.对list进行删除  
语法：list_name.remove(item)  

6.检测list中是否含有某元素  
	>>>x in list_name
	=> False	//x不在list中
	=> True 	//x在list中

###dictionary  
所谓字典就是每个item都是一对key-value对。通过key获取value  
与list类似，dictionary同样是mutable。比如：  
	//声明一个新dictionary
	dict_name = {'a':1, 'b':2}
	//添加新的key-value对,如果key存在，相当于重新赋值
	dict_name[new_key] = new_value
	//删除一对key-value
	del dict_name[key_name]

###其他  
1.float():强制转换为float类型  
	a = 1
	b = float(a)	//b = 1.0

2.对于由数值构成的list，求和可以直接使用sum()  
	result = sum(list)

3.

