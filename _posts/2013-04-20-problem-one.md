---
layout: post
title: "已知a[N],求b[i]=a[0]*a[1]..a[N]/a[i]"
description: ""
category: 面试题
tags: C/C++
---
{% include JB/setup %}

##问题描述  
已知一个数组a[N]，构造一个数组b[N]，构造规则：b[i]=a[0]*a[1]*a[2]...a[N]/a[i];  
要求：1.不可以用除法  
      2.时间复杂度为O(n)，空间复杂度为S(1)  
      3.除遍历使用的变量外，不可以使用其它变量  

###思路描述  
线性时间内，构造：  
b[i]=a[0]*a[2]...a[i]  
a[i]=a[i]*a[i+1]...a[N-1]  
最后b[i]=b[i-1]*a[i+1]  (i=1,2,3...,N-3,N-2)  
b[0]=a[1],b[N-1]=b[N-2].

###源代码  
	void produce_b_by_a(int *a, int *b, int N)
	{
		int i;
		b[0]=a[0];
		for(i = 1, i < N; i++){
			b[i] = b[i-1] * a[i];
		}
		for(i = N-2; i >= 0; i--){
			a[i] = a[i] * a[i+1];
		}
		for(i = 1; i < N-1; i++){
			b[i] = b[i-1] * a[i+1];
		}
	}

