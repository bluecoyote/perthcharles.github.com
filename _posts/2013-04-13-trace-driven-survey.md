---
layout: post
title: "Trace驱动的memory模拟：综述"
description: ""
category: papars
tags: trace
---
{% include JB/setup %}

#论文来源  
	(在google scholar中搜索：trace-driven memory simulation a survey )
	#wget http://www.cs.amherst.edu/~sfkaplan/courses/spring-2004/cs40/papers/UM:TDMS.pdf
博客里面写的只是粗略的理解，错误难免。想更准确的了解还是请看论文原文。
#简介  
处理器速度与memory速度之间的差距越来越大，成“剪刀口”型增长趋势。在memory-system设计被硬件实现之前，找到评价memory-system设计的方法显得十分重要。  
其中一种有效的方法就是：通过抓取真实应用的访存trace，然后通过在模拟器上模拟抓取下来的trace行为达到测试memory-system的性能效果。下面将根据前面提到的论文，适当整理思路，以便之后学习。  
所谓访存trace，就是一系列的对内存进行访问的操作序列（a sequence of memory references）
***  
##主要难点  
	1，收集完整的trace信息很难。特别是对于多进程，操作系统，动态链接或动态编译产生的访存trace很难获取。
	2，访存trace一般很大。一般都是10G～100G这个量级的。

##Trace driven memory simulation主要流程  
	1，trace collect：	收集某些选定负载的访存序列。
	2，trace reduction:	由于trace文件一般都很大，如果模拟完成的trace将会十分耗时。通过去除不需要、冗余或是不感兴趣的数据来提高整体的效率。
	3，trace processing:	将得到的trace文件当初输入给模拟器处理
##对各类方法的评价标准  
	准确性：	模拟出来的性能与真实性能之间的差距；reduction之后的trace模拟结果与完成trace模拟结果之间的差异等
	速度：		每秒收集到的trace entry个数（无法跨平台对比）；entry收集速度/entry产生速度;entry processing速度/entry产生速度；总模拟时间/正常执行时间
	额外的内存开销
	reduction 比例
	portability,flexibility,expense,easy-of-use
###Trace collect  
评价trace质量的标准主要就是：完整性和详细性。另外在收集过程中，不得收录额外引起的访存动作，主要就是收集工作本身产生的访存动作不应该被收录到trace中  
	完整性：所有的访存动作都要收集，包括所有用户级进程和操作系统内核产生的访存动作。
	详细性：是否给trace添加一些额外的信息，比如VM page-table状态，访存动作类型（读，写，执行），大小（字，半字，字节等）
一般的工具在收集的时候如果trace buffer写满了，都需要停下来将buffer里面的数据导出到外部。  
各种工具收集方法：  
	trace收集方式的不同主要体现在收集动作对应系统层次的不同
	------------软件层次-------------
	| 	操作系统级的单步执行	|
	| 	编译器			|
	| 	汇编器			|
	| 	连接器和加载器		|
	|--------------------------------
	|	微指令			|
	|--------------------------------
	|	物理层：探测物理信号	|
	---------------------------------
###Trace reduction  
各类方法的主要不同在于reduction比例的不同和reduction方式  
	主要reduction方式：
	压缩：		利用标准的数据压缩算法对数据进行压缩（觉得这种方法不实用）
	重要事件：	在收集trace的时候只收集满足一定条件的trace，详见论文
	过滤：		由于每个研究人员的研究兴趣重点不同，想要模拟的trace类型也就不同
	抽样：		分时间抽样和集合抽样。（这种方法使用组内开发的工具：HMTT实践过）
###Trace processing  
因为memory-system设计的多样性（页面替换算法、cache大小、写策略：写穿透等，line大小），所以在将trace输入到模拟器时，自然就想一遍输入，就能跑几种不同的配置方式。为了达到这个目的就导致来trace processing方式的多样性。  

***  
转载请注明出处。  
版权所有，侵犯必究  
***  
