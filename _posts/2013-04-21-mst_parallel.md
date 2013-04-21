---
layout: post
title: "并行最小生成树算法"
description: ""
category: 图论 
tags: MST
---
{% include JB/setup %}

##论文  
A distributed algorithm for minimum-weight spanning tree By:PG Gallager  

##重要定理  
最小生成树重要定理：  
	一个点的最小边一定是在最小生成树中的。
利用反正法能很快证明。  

##算法步骤  
1.找到每个点对应的权值最小的边。  
2.完成步骤1后，原图会被分割成若干个部分。每个部分用一个点代替，各个部分之间可能会存在多条边，仅保留权值最小的那条来表示相应两个部分的距离。  
3.完成步骤2后，得到一个缩减后的图。重复前两个步骤直到缩减后的图只有一个节点。  
###图示  
![算法图示](/assets/images/222.png)  

##MapReduce模型并行算法  
要说明的一点是各个节点是否属于同一个部分，利用并查集实现。初始化时，每个节点对应一个集合，随着迭代次数的增加，集合的数量会快速减少。
***  
	Mapper
	输入：(src, dest:weight)
	输出：所有(src_setno, dest_setno:weight),其中src_setno != dest_setno
	注解：src_setno表示src节点所在集合。对于输入进来的src_setno == dest_setno的边直接删除，因为这些边很显然是多余的。从而提高效率
***  
	Reducer
	输入：(src_setno, dest_setno:weight)
	输出：1.对于src_setno相同的输入，保留weight最小的那条边到最终的解集合中
	      2.将保留边相应两个顶点所在集合进行合并
***  
###缺点  
需要在每个节点维持并查集，而且reduce过程要对并查集进行写操作，这里可能成为性能瓶颈。
***  
###进一步改进  
在mapper与reducer之间添加combiner  
因为两个集合之间可能有多条边，这样Mapper可能产生很多src_setno，dest_setno都相同的输出。通过combiner将这类型的输出进行合并，只保留weight最小的输入。减少Reducer需要处理的数据量  

***  
转载请注明出处  
版权所有，侵犯必究  
***  

