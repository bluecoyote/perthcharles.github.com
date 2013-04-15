---
layout: post
title: "linux 反汇编初步"
description: ""
category: 
tags: 反汇编
---
{% include JB/setup %}

##工具  
十六进制编辑器：hexedit  
objdump:

***  
###hexedit使用  
暂时只用hexedit来读二进制文件  
	#hexedit filename  //查看文件  
常用操作键  
       Ctrl-X: save and exit  
       Ctrl-C: exit without saving  
       tab:	在hex和ascii窗口之间切换  
       Ctrl-U: undo all  
       Ctrl-S: search forward  
###objdump使用  
编译程序的时候，gcc添加-g选项，增加调试信息  
	#gcc test.c -g -o test
常用参数  
	-S(source):表示读取哪个文件
	-j:选择读出哪个section，可以通过objdump -h来查看所有的section
***  
***  
###看懂AT&T汇编  
由于objdump反汇编得到的结果主要都是AT&T格式的汇编(不过好像可以选择？)，而且linux内核代码也有不少AT&T格式的汇编代码，所以有必要学习一下  
####AT&T汇编特点  
	1.寄存器前面要加%，如：mov %eab,%ebx
		注意源寄存器和目标寄存器的顺序与intel汇编更好相反，at&t中左边是源寄存器，右边是目标寄存器。所以上面指令是将eax的值赋给ebx
	2.立即数/常数前面要加‘$’,符号常数值直接用。
		关于符号常量注意理解下面两句：
		mov A,%eax 	//将A代表的值赋给eax,如A=10，则eax里面的值就是10
		mov $A,%eax 	//将A代表的值当作地址，将对应地址的值赋给eax，如A=0x10,0x10处存则20，则把地址0x10处对应的值20赋给eax
	3.movb:8位(byte)	movw：16位(word)	movl：32位(long)  
	others:	s=short(16-bit integer) or single(32-bit floating point)
		q=quad(64 bits)
		t=ten bytes(80 bits floating point)
	注：如果suffix没有指定且不是内存操作，GAS(Gnu AS)会根据目标寄存器的大小来决定
	4.call/jmp语句的操作数前面要加上“*”作为前缀，远跳转ljmp,远调用lcall，远返回lret

	5.寻址规则：displacement(base register, offset register, scalar multiplier)
	  计算方法：(base+dis)+(offset*multiplier)
	  举例：
		movl    -4(%ebp, %edx, 4), %eax  # Full example: load *(ebp - 4 + (edx * 4)) into eax
		movl    (%ecx), %edx             # No offset: copy the target of a pointer into a register
####C语言内嵌汇编  
格式：  
	_asm_("asm statement":outputs:inputs:registers-modified)
tips:
	1.在嵌入汇编中，寄存器前面要加两个%，因为gcc在编译时，会去掉一个%再输出成汇编格式
####主要寄存器及其作用  
#####8086有14个16位寄存器，按照用途分为：  
1.通用寄存器(8个)  
2.指令指针(IP,1个)  
3.标志寄存器(FR，1个)  
4.段寄存器(4个)  
***  
*通用寄存器*又可以分成2类：数据寄存器和指针寄存器及变址寄存器，各4个  
	ax:常用于计算。另外所有的I/O指令都使用这一寄存器与外界设备传送数据
	bx:基址寄存器  
	cx:计数寄存器  
	dx:数据寄存器  
	
	SP:堆栈指针，与SS配合使用，可指向目前的堆栈位置  
	BP:基址寄存器，可作为SS的相对基址位置  
	SI:source index,源变址寄存器------暂不理解  
	DI：destination index,目的变址寄存器  
	上面四个寄存器只能按16位进行操作，主要用来形成操作数的地址  
*指令指针IP*  
	IP:16位专用寄存器，用来指向当前执行指令的下一条指令的地址。注意，IP指向的是指令地址的段内地址偏移量  
*标志寄存器FR*  
16位的寄存器，有意义的有9位，6位是状态位，3位是控制位  
分布图：  
	#################################################
	#  #  #  #  #OF#DF#IF#TF#SF#ZF#  #AF#  #PF#  #CF#
	#################################################
	#15#14#13#12#11#10# 9# 8# 7# 6# 5# 4# 3# 2# 1# 0#
	#################################################
	各个标志的含义：  
	OF:overflow  
	DF:direction
	IF:中断允许标志，标志是否响应CPU‘外部可屏蔽‘中断，1表示响应
	TF:跟踪标志
	SF:符号标志，与运算结果的最高位相同
	ZF:零标志，反映运算结果是否为0
	AF:辅助进位标志
	PF:奇偶标志反映运算结果中’1‘的个数，PF=1表示偶数个’1‘
	CF:进位标志反映运算结果是否产生进位或借位
*段寄存器*  
	CS:code segment
	DS:data segment
	SS:stack segment
	ES:extra segment
***  
####80386寄存器  
寄存器都是32位宽  
*通用寄存器*  
	EAX，EBX，ECX，EDX
*特殊寄存器*  
	ESI：通常在内存操作中作为“源地址指针”使用，DS是默认段寄存器
	EDI：通常在内存操作中作为“目标地址指针”，DS是默认段寄存器
	EBP：通常被高级语言编译器用以建造‘堆栈帧’来保存函数或过程的局部变量，SS是默认段寄存器


***  
###主要参考资料  
[汇编中各寄存器的作用-堂吉歌德](http://www.cppblog.com/tdweng/articles/120852.html)  
[X86 Assembly/GAS Syntax](http://en.wikibooks.org/wiki/X86_Assembly/GAS_Syntax)  
***  
