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

###更进一步  
将下面代码反汇编，查看取反操作是否是上面的说法：按照32位取反  
	#include<stdio.h>
	int main(void)
	{
		unsigned char a = 0xa5;
		printf("%d\n",~a);

		return 0;
	}

	#gcc test.c -o -g test 
	#objdump -S test > test.debug
	#cat test.debug
	...
	00000000004004c4 <main>:
	#include<stdio.h>
	int main(void)
	{
	  4004c4:	55                   	push   %rbp
	  4004c5:	48 89 e5             	mov    %rsp,%rbp
	  4004c8:	48 83 ec 10          	sub    $0x10,%rsp
	    unsigned char a = 0xa5;
	  4004cc:	c6 45 ff a5          	movb   $0xa5,-0x1(%rbp)
	    printf("%d\n",~a);
	  4004d0:	0f b6 45 ff          	movzbl -0x1(%rbp),%eax
	  4004d4:	89 c2                	mov    %eax,%edx
	  4004d6:	f7 d2                	not    %edx
	  4004d8:	b8 f8 05 40 00       	mov    $0x4005f8,%eax
	  4004dd:	89 d6                	mov    %edx,%esi
	  4004df:	48 89 c7             	mov    %rax,%rdi
	  4004e2:	b8 00 00 00 00       	mov    $0x0,%eax
	  4004e7:	e8 cc fe ff ff       	callq  4003b8 <printf@plt>
	
	    return 0;
	  4004ec:	b8 00 00 00 00       	mov    $0x0,%eax
	}
	...
可以看到指令"not %edx"是直接按照32位进行取反的  
如果对程序进行-O2优化编译的话，就看得更直观  
	#gcc -O2 test.c -g -o test-O2
	#objdump -S test-O2 >test-O2.debug
	#cat test-O2.debug
	...
	00000000004004d0 <main>:
	#include<stdio.h>
	int main(void)
	{
	  4004d0:       48 83 ec 08             sub    $0x8,%rsp
  	     unsigned char a = 0xa5;
	     printf("%d\n",~a);
	  4004d4:       be 5a ff ff ff          mov    $0xffffff5a,%esi
	  4004d9:       bf e8 05 40 00          mov    $0x4005e8,%edi
	  4004de:       31 c0                   xor    %eax,%eax
	  4004e0:       e8 d3 fe ff ff          callq  4003b8 <printf@plt>
	
	     return 0;
	}
	...
可以看到程序直接将0xffffff5a赋给esi寄存器了  
###我本子相关信息  
	#uname -r
	2.6.32-358.el6.x86_64
	#gcc -v
	gcc version 4.4.7 20120313 (Red Hat 4.4.7-3) (GCC)

