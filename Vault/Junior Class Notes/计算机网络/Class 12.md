Q
1. 什么是路由，什么是转发？
ans：p279
2. 路由算法通常如何分类？
ans：动态静态
3. 汇集树是什么？
ans：作为最优化原则的一个直接结果,从所有的源到一个指定目标的最优路径的集合构成了一棵以目标节点为根的树。
一种优化的准则
4. 距离矢量路由算法的基本含义？
ans：p285
5. 链路状态路由-什么是链路状态？对链路状态的理解 state代表
6. 链路状态路由用什么协议？
ans：OSI


### 5.3 Congestion Control 网络层的拥塞控制——理解即可
网络层的上方是传输层
**网络层和传输层共同承担着处理拥塞的责任。**

然而,控制拥塞的最有效方法是减少传输层注入网络的负载。这就需要网络层和传输层共同努力协同工作。——互相协调的结果


- Congestion results when too much traffic is offered
- Performance degrades due to loss and retransmissions
- Goodput trals offered load
会有数据拥堵的恶性循环：时间到期后会以为丢失而在此发送，++

- General Principals
	- Monitor the system and 

- Approches:
- Traffic Aware Routing 流量感知路由
- Addmision Control 准入控制
	with virtual circuits
	Can combine with traffic-aware routing 

- 流量调节：
- Traffic Throttiling 显示拥塞控制


- 负载脱落

理解这些能在网络层做拥塞控制的措施
考：列举拥塞控制的措施 etc.

## 5.5 Internetworking 网络互联——理解即可
数据链路层的互联：网桥 交换机

Internet working merges mutilple,different networks to form a single larger network 
*Internet和internet含义是不同的*

### Tunneling 隧道
网络层就是用来进行传输的

### Packet Fragmentation 数据包分段
- 透明分段：中间路由器不做分段的重组
- 非透明分段：
因特网的网络层叫IP层

问：因特网IP的分段方式
为什么要互联 采用什么设备
互联中存在什么方式 分段

## 5.6 Network Layer in the Internet因特网网络层
### IPv4 Protocol
IPv4的地址长度：32位（bits）

书p340
与以太网地址不同的是I P 地址具有层次性。每个3 2 位地址由高位的可变长网络和低位的主机两部分数据组成。


网络号+主机号

子网掩码：目的是为了切分网络号和主机号
255.255.255.0=三个字节表示网络号 一个字节表示主机号
再使用与操作来分开两部分的号码内容

### 分类和特殊寻址
A，B，C类地址

### 











