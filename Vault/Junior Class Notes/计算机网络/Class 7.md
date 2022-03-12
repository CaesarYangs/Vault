## **Q&As：** #CN_QAs
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

# Chapter 3  Data Link Layer
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

### Utopian Simplex Protocol 乌托邦式单工协议
an Ideal protocal
- no errors,receivers runs fast as sender
- Only one-way data transfer
协议慢慢从理想走到现实

### Stop-and-Wait Protocol for Error-free 无错信道停等协议
Ensures that sender never outpaces receiver
- receiver retuners a dummy frame when ready
- Only one frame outstanding at a time, thus called stop-and-wait
- Flow control is added

## Stop-and-Wait proticol for noisy 有错信道停等协议
- ARQ(automatic repeat request) adds error control 自动重复请求
	- receiver replies with an "ack" frame for the frame that has been correctly received
	- Sender sets timer and retransmits a frame if the expected "ack" is not received
- To ensure correctness, frames and acks must be numbered 

### Sliding Window Protocols 滑动窗口协议
#### Concept 
- Sender maintains window of frames that it can send
	- it needs to buffer the frames for possible retransmission
	- Window advances with next acknowledgements
- Receiver maintains window of frames it can receive
	- It needs to keep buffer space for arrivals
	- Window advances with in-order arrivals
- Larger windows would enable pipeling for efficient use of the link


#### One-bit sliding window protocol 1位滑动窗口协议
Piggyback
#### Using "GO Back N" 回退N协议
Receiver only accepts/acks frames that arrive in order

Receiver discards frames that follow a missing/error frame

Sender times out and resends all outstanding frames
有延迟存在
#### Using "Selective Repeat" 选择重传协议
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

物理介质层和真正的层