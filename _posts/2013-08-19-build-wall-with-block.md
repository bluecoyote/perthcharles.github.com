---
layout: post
title: "木块砌墙问题"
description: ""
category: 面试题
tags: []
---
{% include JB/setup %}

##题目  
用1x1x1,1x2x1以及2x1x1的木块搭建高长宽为Kx2^Nx1的墙，不能翻转、旋转。  
题目来源：[木块砌墙问题](http://blog.csdn.net/dw14132124/article/details/9038417#t2)  

##思路分析  
1.由于厚度固定为1，可以直接降维度。变为：  
用1x1,1x2和2x1的矩形填充大小为Kx2^N的矩阵。  
2.
