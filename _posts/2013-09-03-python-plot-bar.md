---
layout: post
title: "[python实践]使用matplotlib库画宽度可变的条形图"
description: ""
category: python
tags: 
---
{% include JB/setup %}

##相关库安装  
	#yum list |grep numpy
	#yum install numpy

	#yum list |grep scipy
	#yum install scipy

	#yum list |grep matplotlib
	#yum install python-matplotlib

##直接上脚本  
	#cat test.py
	import pylab as pl
	import numpy as np
	//读取文本中的数据
	data = np.loadtxt('filename')
	#width = 0.5
	width = data[:,1]/1000   //设置条形图中每个柱子的宽度
	//以data第一列为X轴，data第二列为Y轴，每个柱子的宽度设置为第二列值的千分之一
	pl.bar(data[:,0], data[:,1], width)
	pl.show()


##参考资料  
[NumPy Reference](http://docs.scipy.org/doc/numpy/reference/index.html)  
[Python图表绘制：matplotlib绘图库入门](http://www.cnblogs.com/wei-li/archive/2012/05/23/2506940.html)  
[MATLAB中subplot的用法](http://blog.sina.com.cn/s/blog_5fef8a5a0100duzf.html)  
[Cookbook / Matplotlib / BarCharts](http://wiki.scipy.org/Cookbook/Matplotlib/BarCharts?highlight=%28bar%29)  
[Matplotlib Examples v1.3.0](http://matplotlib.org/1.3.0/examples/index.html)  
[Matplotlib tutorial](http://www.loria.fr/~rougier/teaching/matplotlib/)  


