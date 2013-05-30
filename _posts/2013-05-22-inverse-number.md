---
layout: post
title: "POJ上看到一种O(nm)求逆序数的方法"
description: ""
category: 
tags: []
---
{% include JB/setup %}

#思路其实很简单，直接上代码  
	int count_inver(char *str, int len)
	{
	        int i;  
	        int cnt = 0;
	        int a[4] = {0};
	        for(i = len - 1; i >= 0; i--) {
	                switch (str[i]) {
	                        case 'A':
	                                a[1]++; 
	                                a[2]++; 
	                                a[3]++; 
	                                break;  
	                        case 'C':
	                                a[2]++; 
	                                a[3]++; 
	                                cnt += a[1];
	                                break;  
	                        case 'G':
	                                a[3]++; 
	                                cnt += a[2];
	                                break;  
	                        case 'T':
	                                cnt += a[3];
	                }
	        }
	        return cnt;
	}
	
#算法分析  
时间复杂度是O(mn)，其中m表示所有可能出现元素的个数，比如上例只可能出现“A,C,G和T”，那么m=4，而n表示该字符串的长度。由于m一般来讲比n小很多，所以这种以空间换时间的算法还是挺有效果的。  

