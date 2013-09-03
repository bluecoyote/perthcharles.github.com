---
layout: post
title: "[编程之美]控制CPU使用率曲线"
description: ""
category: 面试题
tags: C/C++
---
{% include JB/setup %}

###闲聊  
由于我的电脑被WIN7鄙视(跑WIN7显得比较慢)，同时如果按照原书中的代码需要掌握相当的WINDOWS API，对于这点目前我同样是做不到的。所以必须摸索一种LINUX下的方法完成类似的任务。  
程序的思路应该不难理解，CPU使用率曲线是*刷新间隔内CPU的平均使用率*。同时需要确认你的电脑CPU是几核的。比如我的电脑是双核的，则跑一个while(1)的话，CPU使用率只会达到50%。这点验证代码如下(shell)：  
	#cat 50-percent-cpu.sh
	#!/bin/bash
	while [ 1 ] 
	do
	:	
	done
	//注:shell空语句必须填上，在bash里冒号“:”表示空语句
###linux下实现  
我机器System Monitor更新CPU History的频率大概是1s(通过观察下方CPU1和CPU2使用率刷新频率得出)  
如果将正弦曲线周期设置为40s，则至少需要制作40份不同的CPU使用频率出来。  
对于特定值的CPU使用率，比如30%，则需要让CPU在1s内睡眠700ms, 执行while(1)300ms。至此具体的实现方法应该逐渐清晰了。  
代码请见我github codeware仓库中的[sine-cpu.c](https://github.com/PerthCharles/codeware/blob/master/sine-cpu.c)。简单说明在用gcc编译的时候，由于用到了sin函数，所以需要加入-lm选项。即:  
	#gcc -lm sine-cpu.c -o sine-cpu
跑的时候使用taskset将程序设置到一个CPU上跑  
	#taskset -c 0 ./sine-cpu
###遇到问题  
1.使用库函数请一定包含全部正确的头文件。  
2.忙闲时间控制体现在:busy[i] = (double)(base_line + base_line*sin(w*i))；  

