---
layout: post
title: "中国剩余定理"
description: ""
category: 面试题 
tags: 数论
---
{% include JB/setup %}

##问题  
一个整数除以三余二，除以五余三，除以七余二，求最小的满足条件的整数  

##要点  
各个除数之间要互质  

##解法要点  
求出5和7的最小公倍数35的倍数中除以3余数为1的最小一个70（这个称为35相对于3的数论倒数），3和7的最小公倍数21相对于5的数论倒数21，3和5的最小公倍数15相对于7的数论倒数15，然后  
$$70\times 2+21\times 3+15\times 2=233$$  
但这求出的并不是最小值，因为35%3已经等于2了，所以最终的求解算法应该是：  
$$n=\left( a\ast 10+b\ast 4+c\ast 15\right) \%105$$  
求模是因为如果存在一个比105大的可行解，则必然存在一个比105小的可行解。
然后根据题目要求确定满足条件的n。

##C代码  
	#include<stdio.h>

	//get_m()的作用就是求a*b 相对与c 的数论倒数
	int get_m(int a, int b, int c)
	{
		int ab, ab_r;
		int i, j;
		ab = a*b;
		ab_r = ab%c;
		j = ab;
		for(i = 0; i < c; i ++){
			if(ab % c == 1)
				return ab;
			else
				ab += j;
		}
		return -1;
	}
	
	int main()
	{
		int a, b, c, n;
		int a_r, b_r, c_r;	//a_r是n%a的余数
		int a_m, b_m, c_m;	//a_m是(b*c)相对与a的数论倒数
		scanf("%d %d %d", &a, &b, &c);
		if(a*b*c == 0){
			printf("you must be kidding me!\n");
			return 0;
		}
		scanf("%d %d %d", &a_r, &b_r, &c_r);
		if((a_m = get_m(b, c, a)) != -1 && (b_m = get_m(a, c, b)) != -1 && (c_m = get_m(a, b, c)) != -1){
			printf("n is:%d\n", (a_m*a_r + b_m*b_r + c_m*c_r) % (a*b*c));
			return 0;
		}
		else{
			printf("Can not find an answer!\n");
			return 0; 
		}
	}

##参考资料  
[中国剩余定理](https://zh.wikipedia.org/zh-hans/%E4%B8%AD%E5%9B%BD%E5%89%A9%E4%BD%99%E5%AE%9A%E7%90%86)  

