
- Q1: 有没有没有冲突的协议 
ans：令牌协议
- Q2：隐藏终端
ans：在感知范围之外
- Q3：暴露终端的导致
ans：两个节点太接近了
- Q4：以太网的分类 它们之间的介质访问控制协议是一样的吗？
ans：经典 快速。不一样
- Q5：经典以太网mac层用什么协议
ans：CSMA/CD
- Q6：为什么经典以太网要求所有数据帧用2倍t来传输
ans：短帧问题 没法坚持到 p220
- Q7：CSMA/CA冲突避免的方式
ans：主动后退 p235
- Q8：CSMA/CA通常采用什么方式来判断是否发生冲突
ans：利用确认的方式推断 ACK

不同的backoff时长来支持不同的cos

### 
不同level的backoff目的是提供不同的服务
- Different back off slot times support quality of service
	- Short intervals are given to preferred access e.g. control VoIP
- MAC also has other mechanisms e.g. power save


### 802.11 Frames
数据帧 控制帧 管理帧 


## 4.8 Data Link Layer Switching  数据链路层交换
- 在数据链路层的角度进行网络连接和更大互联
- 网桥和交换机的概念
### Users of bridges
- Multiple LANs can be connected by bridges to handle load that is higher than the capacity of a single LAN
在数据链路层进行互相的连接
广播方式：如果station发现数据接收方/目的地不是自己就扔掉 

### * learning bridges 后向学习 
建表后通过后向学习：就是简单的不停地在节点之间发送广播，接收，判定，将网桥内的表学习填满。
Bridge工作的环境在

### Repeaters,hubs,bridges,routers and gateways
数据链路层用Bridge和switch
网络层用Router



# Network Layer
Responsible for delivering packets between endpoints over multiple links.
网络层的上层是传输层

## Design Issues

### Store-and-forward Packet Switching
- Hosts send packets into the network
- Packets are forwarded by routers

上层给下层提供服务
下层给上层提供接口

### Connectionless Service - Datagrams 无连接的服务-数据报的实现
- A packet is forwarded using destination address inside it
- Different packets may take different paths
提供给相邻节点的连接 因为网络是逐跳的
动态适应网络状态变化
> I P 协议是整个Internet的基础,它是无连接网络服务的重要范例。每个数据包携带一个目标I P 地址,路由器使用该地址来单独转发每一个数据包。

重点p277 5.1.4上方部分 #计算机网络考点 

### Connection-Oriented Service - Virtual Circuits
VC在internet上用的不是很多
- A packet is forwarded along a virtual circuit using tag inside it
- Virtual circuit (VC) is set up ahead of time

正式传输数据之前先进行setup 预留部分
先用特殊的消息进行传递 将线路线进行保留 后续所有的数据都在这条路径上走
通过打标签的方式让路由在虚拟链路上传递data——虚拟链路号
在数据网里面经常使用



