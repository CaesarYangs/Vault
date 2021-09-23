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

### OSI Reference Model
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


### TCP/IP Reference