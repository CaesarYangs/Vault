### Overview



## Introduction
- Computer network
	-  A number of individual computers interconnected through a communication network
	-  A collection of autonomous computer systems interconnected using a single technology
- Computer Network VS. distributed system
	- Distribute System:
	An abstraction for computation or data processing 

- Transmission Technologies
	- Broadcast transmission---smaller,geographically,localized
	- Point-to-point transmission---large,wide area

### Network Software
#### Protocol Hierarchies
> 使用协议栈 分层的根本原因：降低网络 设计的复杂度


Q&As：
- 使用协议栈的原因？
- 协议栈的定义？
- 虚线实现代表啥？虚线不是直接通信的结构 实线代表进行真实的通信
- 可靠的代表什么？ack 有确认的数据报服务
- 为什么要用不可靠连接？用不可靠服务上层的可靠层来保证服务的正确执行。可靠建立在不可靠之上；减少延迟等

#### Design Issues for the Layers
- Addressing 寻址
- Error control 纠错
- Flow control 流量控制
- Multiplexing 复用
- Routing 路由

network architecture

primitive-原语

### OSI Reference Model_七层模型
- A principled,international standard,seven layer model to connect different layers.
1. Physical 物理层
	Sends bits as signals
2. Data Link 链路层
	Sends frames of information
3. Network 网络层
	Sends packets over multiply links
4. Transport 传输层
	Provides end-to-end delivery
5. Session 会话层
	 links Manage task dialogs
6. Presentation 表示层
	Makes different representations 
7. Application 应用层
	 Provide funcitons needed by users

PDU一协议数据单元

在网络中通过下面三层进行主机间的通信

### TCP/IP Reference ＿四层结构
针对七层模型合并
*核心网接入网
1. 应用层
2. 传输层
3. 互联网层
Omit some OSI layers and uses the IP as the network layer
向上兼容：
可以使用不同的应用层网络传输协议。支持因特网的应用是非常扩展的。
向下兼容：
用户互联网接入方式在不断变化，从主机到网络的基于IP和ICMP的接入方式可以不断扩展。

### A Comparison of OSI and TCP/IP Mode
- Concepts central to the models
	- Services服务
	- Interfaces接口
	- Protocols协议
- OSI
Very influential model and clear concepts
- TCP/IP
Very successful protocols that worked well and thrived to become a defacto standard

### Example Networks
- Internet
**ISP networks serve as the Internet backbone**
不是单一的网络 是大量不同网络的集合
网中网

- Ethernet 
- 3G
Cellular network is based on spatial cells
IP层以上的协议层很重要
- WLAN:802.11
- Emerging Network












