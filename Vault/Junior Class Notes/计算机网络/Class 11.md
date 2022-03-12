## Q&A
- Q1:网桥的主要作用是什么？是哪一层的网络内容？
ans：    属于数据链路层
- Q2: Learning Bridges 的ppt 网桥扩展数据链路层 下面两句话的理解 说明什么意思
ans：网桥使用但不去除头。因为网桥属于数据链路层 不能管网络层以上的相关知识
- Q3: 如何体现存储和转发（数据包交换）两个词的含义？
ans：
- Q4: 因特网的IP协议是无连接和有连接服务？
ans：无连接
- Q5: 虚电路的基本思想 为什么需要虚电路网络？
ans：隐藏在虚电路背后的思想是避免为每个要发送的数据包选择一条新路径
- Q6: 虚电路和数据包在路由上有什么不同
ans：p274 还有本章小结p376




## 5.2 Routing Algorithm 路由算法
路由
即发现一条网络的路径 到目的地的路径

做法：model建模 路径由不同的节点组成
进而优化节点组合
当网络动态变化的时候还需要进行自适应修改

传不传数据，路由算法和系统都在实时工作。

- Routing is about the discovery of network paths

### The Optimality Principle 优化原则
- Each portion of a best path os also a best path 
- Sink Tree 汇集树
The union of all the best paths to a router
作为最优化原则的一个直接结果,从所有的源到一个指定目标的最优路径的集合构成了一棵以目标节点为根的树。
- 跳数：距离度数

**所有路由算法的目标是为所有路由器找到这样的汇集树,并根据汇集树来转发数据包。**

### Shortest Path Routing 最短路径算法
有不同的路径计算方法：跳数，两点间平均时延

### Flooding 泛洪算法
- A simple method to send a packet to all network nodes
- 泛洪算法是一定能够找到一条路由道路的方法


### Distance Vector Routing 距离矢量路由算法--动态路由
距离矢量路由算法是这样工作的z每个路由器维护一张表（即一个矢量）,表中列出了当前己知的到每个目标的最佳距离,以及所使用的链路。这些表通过邻居之间相互交换信息而不断被更新,最终每个路由器都了解到达每个目的地的最佳链路。

- Distance vector is a distributed routing algorithm 
Shortest path computation is split across nodes
- Algothrm
	- Each node knows distance of links to its neighbors
	- Each node advertises vector of lowest known distances to all neighbors
	- Each node uses received vectors to update its own
	- Repeat periodically

这些寻找算法都是局部最优算法，不是全剧最优

不同的路由器之间在随时沟通，不管有没有使用者
本身路由器节点到所有节点的路径走法

什么是这两个。     两个基本原理。 因特网中哪些协议使用了这两个？
考点：什么是距离矢量 整体的流程是什么 什么是动态路由 如何进行动态
要知道这两种路由算法在因特网
### Link State Routing 链路状态路由--动态路由
出现原因：距离矢量在使用过程中在存在大量节点时收敛时间趋于∞

- The Algorthm 
	- Each node floods information about its neighbors in LSPs(Link State Packets)
	- All nodes learn the full network graph 
	- Each and every node runs Dijkstra's algorithm to compute the paths to reach other destinations 
	


#### 1 发现邻居
发现邻居操作的实现是通过实时一直广播寻找

#### 2 设置链路成本
在广播的过程中度量成本

#### 3 构造链路状态包
Each node floods information about its neighbors in LSPs(Link State Packets)
每个节点都计算最短路径来调整

#### 4 分发链路状态包
#### 5 计算新路由

网络投递过程中只和它相临的下一个节点来走 不能跳步