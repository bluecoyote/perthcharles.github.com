---
layout: post
title: "BFS和DFS算法温习"
description: ""
category: 图论
tags: []
---
{% include JB/setup %}

##广度优先搜索BFS  
给定无向图G和源点s，遍历图。  
	BFS(G,s)
	for each vertex u in G
		u.color = white  //所有点置为未扫描
	endif
	s.color = black  //设置源点s为当前扫描点
	Q = new queue   //新建空队列
	Q.add(s)	  //加入源点s
	while(Q)
		u = Q.dequeue  //取队列首节点
		for each vertex v connect with u
			if(v.color == white)
				Q.add(v)
				v.color = black
		endif
	endwhile
[广度优先遍历演示地址](http://sjjg.js.zwu.edu.cn/SFXX/sf1/gdyxbl.html)  

##深度优先搜索DFS  
给定无向图G和源点s，遍历图。  
方法一：非递归实现，直接用到栈。  
	DFS(G,s)
		for each vertex u in G  //置所有点为未访问
			u.color = white
		endif
		s.color = black   //置源点为已访问
		T = new stack
		T.add(s)
		while(T)  //只要堆栈不空，就一直找下去
			u = T.top
			if exit v connect with u and v.color is white
				T.push(v)
				v.color = black
			else  //没有未被访问过的链接点后，则当前点u可以出栈了。
				T.pop
			endif
		endwhile
方法二：递归函数实现。其实与方法一无本质区别  
	Main	//主函数
		init(G,s)	//负责初始化G和源点s
		DFS(G,s)
	
	DFS(G,s)
		s.color = black	//标注为已访问
		while(exit v connect with s and v.color is white)
			DFS(G,s)


[深度优先遍历演示地址](http://sjjg.js.zwu.edu.cn/SFXX/sf1/sdyxbl.html)  

