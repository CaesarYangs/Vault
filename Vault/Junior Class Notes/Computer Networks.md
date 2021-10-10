# Computer Networks
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

### OSI Reference Model  七层模型
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

### TCP/IP Reference  四层结构
针对七层模型合并
*核心网接入网
0. 链路层
1. 应用层
2. 传输层
3. 互联网层
Omit some OSI layers and uses the IP as the network layer

- 向上兼容：
可以使用不同的应用层网络传输协议。支持因特网的应用是非常扩展的。
- 向下兼容：
用户互联网接入方式在不断变化，从主机到网络的基于IP和ICMP的接入方式可以不断扩展。

### A Comparison of OSI and TCP/IP Mode
#### OSI
- Concepts central to the **OSI** models
	- Services服务
	- Interfaces接口
	- Protocols协议

> Very influential model and clear concepts
- 无连接和面向连接的通信领域：OSI同时支持。但传输层只支持面向连接通信。
#### TCP/IP
> Very successful protocols that worked well and thrived to become a defacto standard

- 先有协议，TCP/IP模型只是已有协议的一个描述而已===>**模型与协议高度吻合**
- 但TCP/IP不适合任何其他协议栈，描述其他非此的网络，该模型不很有用。
- 无连接和面向连接的通信领域：TCP/IP仅支持无连接一种模式。但在传输层同时支持两种。对于简单的“请求-应答”协议非常重要。

### Example Networks
- Internet
**ISP networks serve as the Internet backbone**
不是单一的网络 是大量不同网络的集合
网中网
- Ethernet 
- 3G
Cellular network is based on spatial cells
必须使用空中接口（Air interface）
IP层以上的协议层很重要
- WLAN:802.11
- Emerging Network

## Chapter 2  Physical Layer
## Chapter 3  Data Link Layer
Main Functionality
- Provide service interface to the network layer
- Transmit frames of information over a single link
	- Handle errors occurred during transmission
	- Regulate the flow of data
		 (Slow receivers don't get swamped by fast senders)
不能出错 流量调节 

## Data Link Layer Design Issue
### Frames
### Possible Services
- Services provided to network layer

路由的目的是应用进程之间的通讯
实现了主机到主机之间网络层面的路由
### Framing Methods
### Error Control
### Flow Control

## Elementary Data Link Protocal






