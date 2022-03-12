## Q&As
Q1：mac层为什么位于数据链路层下部 子层-属于数据链路层
ans：获取信道之后才能进行数据发送的步骤

Q2：信道分配的方法分类 和生活中的例子
ans：静态and动态分配。

Q3：计算机网络是用动态好还是静态好？
ans：通常用动态方式好。静态分配通常在FM收音机  FDM，CDMA
静态式的信道分配不适合于突发的信号分配

Q4：ALOHA是静态or动态？基本的原理是什么？
ans：动态 基本原理：

Q5：ALOHA为什么性能好？
ans：时间槽 错峰发送 减少冲突

Q6：如何进一步减少冲突？
ans：载波监听 CSMA

## CSMA 
(continue [[Class 8#CSMA Carrier Sense Multiple Access 载波监听多路访问协议]])

### CSMA with Collision Detection-带冲突检测的CSMA
即：CSMA/CD——是1-坚持算法
相当于是一种分槽ALOHA
- CSMA improvement is due to aborting transmission upon detecting collision 
	- Reduce contention time to improve performance 
如果一个站检测到冲突，它便立即终止自己的传输，等待一段随机时间，然后重新发送。
CSMA/CD模型将由交替出现的竞争期，传输期，以及所有站都静止的空闲期组成。

- Collision-Free Protocol -- Token Ring 不考 理解即可
传递令牌

## Wireless LAN -Protocal
- Wireless is more complicated compared to wired
- Nodes may have different coverage regions
	- Lead to **hidden** and **exposed** nodes
- Nodes cannot detect collisions, I.e.,sense while sending
	- Makes colllisions expensive and better to be avoided


### Hidden Nodes
- Hidden nodes are senders that cannot sense each other but nonetheless colide at intended receiver 
- Hidden station Problem：由于竞争者太远导致站无法检测到潜在竞争者
### Exposed Nodes
- Exposed nodes ate senders who can sense each other but can still transmit safely(to different receivers)
- Exposed station Problem：两个接收方都不在危险区域，MAC协议防止此类延迟传输的发生

### MACA Mutiple Access with Collision Avoidance Protocol
早期为了解决暴露终端和隐藏终端问题，提出了MACA冲突避免多路访问协议

MACA的基本思想是发送方剌激接收方输出一个短帧,以便其附近的站能检测到该次传输,从而避免在接下去进行的(较大)数据帧传输中也发送数据。这项技术被用来替代载波侦听。
RTS-Ready To Send
CTR-Clear To Send

## Ethernet——介质访问控制自层内知识
现在使用的绝大多数都是交换式以太网 #计算机网络考点 
### Classic Ethernet 经典以太网
- Physicial Layer
- One shared coaxial cable to which all hosts attached

补充padding是为了更好地检测冲突 #计算机网络考点 
- 使用CSMA/CD协议

#### MAC
以太网分为交换式和经典以太网
- Mac protocol is 1-persistent CSMA/CD只有经典以太网使用 #计算机网络考点 
	- Random delay is computed with BEB after collision
	- Frame format is still used in modern Ethernet 交换式以太网也是用这种帧格式

- Collisions can occur and take as long as 2t to detect  最长坚持时间 最坏情况得知冲突时间
	- T is the time it takes to propagate over the Ethernet
	- Leads to minimum packet size for reliable detection 

### Switched/Fast Ethernet 快速以太网
- Hubs join all lines to form a single CSMA domain(冲突域)
- Switched isolate ports to form **separate domains**
	- Much greater throughput for multiple ports
	- No need for CSMA/CD with fulll-duplex lines

hub形式的总线无法同时让多个终端通讯 传统方式只能等待一个结束后再进行
交换机形式可以同时 极大增速

### Gigabit/10Gigabit Ethernet


## Wireless LANs

### 802.11 architecture/protocol stack
- Wireless clients associate to a wired access point(AP)
	- Called infrastructure mode 基础设施模式/有架构模式
	- Without an AP: called ad-hoc mode , but that is the future. 自组织网络


### 802.11 MAC子层协议
- CSMA/CA 即：带冲突避免的CSMA
- CSMA/CA inserts back off slots to avoid collision
- MAC uses ACKs/retransmission for wireless errors
- **使用有确认的无连接服务**