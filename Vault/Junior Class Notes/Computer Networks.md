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


Q&As： #CN_QAs 
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



--- 
## Class 7
**Q&As：** #CN_QAs
- Q1:为什么数据链路层要用帧的形式传播
ans：方便传输 检测错误和纠正错误
- Q2:具体的数据链路层的网络应用：
ans：wifi网络
-Q3: 检测纠错机制的最底层原因
ans：设置数据冗余
- Q4:为什么做流量控制
ans：发送方和接收方的处理信息的速度不一样
- Q5:流量控制的方法
ans：基于反馈 基于控制

## Utopian Simplex Protocol 乌托邦式单工协议
an Ideal protocal
- no errors,receivers runs fast as sender
- Only one-way data transfer
协议慢慢从理想走到现实

## Stop-and-Wait Protocol for Error-free 无错信道停等协议
Ensures that sender never outpaces receiver
- receiver retuners a dummy frame when ready
- Only one frame outstanding at a time, thus called stop-and-wait
- Flow control is added

## Stop-and-Wait proticol for noisy 有错信道停等协议
- ARQ(automatic repeat request) adds error control 自动重复请求
	- receiver replies with an "ack" frame for the frame that has been correctly received
	- Sender sets timer and retransmits a frame if the expected "ack" is not received
- To ensure correctness, frames and acks must be numbered 

## Sliding Window Protocols 滑动窗口协议
### Concept 
- Sender maintains window of frames that it can send
	- it needs to buffer the frames for possible retransmission
	- Window advances with next acknowledgements
- Receiver maintains window of frames it can receive
	- It needs to keep buffer space for arrivals
	- Window advances with in-order arrivals
- Larger windows would enable pipeling for efficient use of the link


### One-bit sliding window protocol
Piggyback
### Using "GO Back N"
Receiver only accepts/acks frames that arrive in order

Receiver discards frames that follow a missing/error frame

Sender times out and resends all outstanding frames
有延迟存在
### Using "Selective Repeat"
- receiver accepts frames anywhere in receive window 
	- Cumulative ack indicates highest in-order frame
	- NAK(negative acks) causes sender retransmission of a missing frame before a timeout resends window 


## Example Fata Link Protocols
### PPP
Frame Flag等等应用到一个具体的协议当中
- a general method for delivering packets across links 
	- Framing uses a flag and byte stuffing
	- Unnumbered mode is used to carry IP packets
	- Errors are detected using a checksum