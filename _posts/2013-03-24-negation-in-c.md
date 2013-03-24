---
layout: post
title: "一道C语言二进制反码题"
description: ""
category: 面试题
tags: C
---
{% include JB/setup %}
###题目  
请写出下面程序在32/64位机器上的输出结果  
编译器：GCC  
	#include<sdtio.h>  

	int main(void)
	{
		unsigned char a = 0xa5;
		printf("%d\n",~a);
		char b = ~a;
		printf("%d\n",b);
		unsigned char c = ~a;
		printf("%d\n",c);
		
		return 0;
	}  

###解答:  
char型数据占一个字节，故  
(a)0xa5 = 1010 0101 = 165  
但是~a并不是a直观的取反，在32位或int长度为4的64位系统中，char和unsigned char 都是按照32位（4字节）取反的，所以这样一来  
(~a) = ~(0x000000a5) = 0xffffff5a//这点可以按照%x格式打印~a验证  
按照%d输出的话，最高位会当成符号位  
所以0xffffff5a先取反得到(符号位除外)  
0x000000a5,然后+1得到//补码与原码的相互转化规则：除符号位外取反再+1  
0x000000a6 = 166  
符号为负，所以第一条打印信息为-166  

解释完第一条打印信息，后两个就好解释了，因为先将~a存入到了char或unsigned char型中，~a取反后的高位被抛弃，所以直接得到0x5a，即90  

###更进一步  todo  
将下面代码反汇编，查看取反操作是否是上面的说法：按照32位取反  
	#include<stdio.h>
	int main(void)
	{
		unsigned char a = 0xa5;
		printf("%d\n",~a);

		return 0;
	}


###我本子相关信息  
	#uname -r
	2.6.32-358.el6.x86_64
	#gcc -v
	gcc version 4.4.7 20120313 (Red Hat 4.4.7-3) (GCC)
编译命令  
	#gcc test.c -o test

