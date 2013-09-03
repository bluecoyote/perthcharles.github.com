---
layout: post
title: "使用matlab从excel文件中读取指定数据，并画图"
description: ""
category: coding
tags: matlab 
---
{% include JB/setup %}

###问题描述  
在matlab下，直接读取EXCEL文件中的数据，并根据指定的数据画图  

###步骤  
1.读EXCEL数据  
主要用到xlsread函数，之所以要写下来是因为读取特定行的方法在帮助文件里面没有提到。  
  读取指定列，比如C列  
  A = xlsread('test.xls', 1, 'C:C');  
  这样就能够直接读取除第C列的数据，且自动去掉标题！  
  更多的普通用法可以查看help xlsread  
2.画图  
根据指定间隔，画出二维图或散点图  

###代码文件  
该Matlab代码通过函数的形式实现，具有一定的移植性，并可以根据实际需要进一步调整。返回值分别是读取的数据总数和用于画图的数据总数。  
[Matlab 代码](https://github.com/PerthCharles/codeware/blob/master/plant_a_array.m)  

