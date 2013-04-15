---
layout: post
title: "Gnu AS 汇编实践"
description: ""
category: 
tags: 汇编
---
{% include JB/setup %}


###首先尝试一个最近简单的Hello world程序  
	#include <stdio.h>

	int main(void) 
	{
    		printf("Hello, world!\n");
    		return 0;
	}
保存文件：hello.c  
	#gcc hello.c -o hello
	#./hello
	Hello World!
产生等价的32位X86 汇编语言程序  
	#gcc -S -m64 hello.c  //将m32改位m64，因为我的机器是64的
	#ls hello*
	hello  hello.c  hello.s
可以看到产生来与hello.c等价的汇编语言程序hello.s,下面用gcc编译这个汇编程序  
	#gcc -m64 hello.s -o hello-asm
	#./hello-asm
	Hello World!

	
