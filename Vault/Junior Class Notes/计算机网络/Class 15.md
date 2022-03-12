Q&As
1. 传输层的主要作用？
2. 端口的作用？
3. 解释加法递增，乘法递减图。什么是最优点？效率线 公平线 迭代的过程如何体现 寻优过程
4. 因特网的传输层两个协议 UDP TCP是什么协议
5. 如何理解TCP在不可靠的互联网上提供可靠的端对端连接


### TCP Connection State Modeling
- Solid lines
	- The normal path for a client
- Dashed lines
	- The normal path for a server
- Light lines
	- unusual events
- Transition

### TCP Sliding Window
在建立连接后处理发送和接收数据的问题

### TCP Timer Management
- TCP estimates retransmit timer from segment RTTs
	- Tracks both average and variance
	- Timeout is set to average plus 4 times the variance

### ==TCP Congestion Control==
- TCP uses AIMD with loss signal to control congestion 
	- Implemented as a congestion window(cwnd) for the number os segments that may be in the network 
	- Uses several mechanisms that work together 

- Congestion window controls the sending rate 
	- Rate is cwnd/RTT
	- Window can stop sender quickly
	- ACK clock(regular receipt of ACKs) paces traffic and smooths out sender bursts
存储转发

- Slow start goes congestion window exponential
	- Doubles every RTT while keeping ACK clock going 