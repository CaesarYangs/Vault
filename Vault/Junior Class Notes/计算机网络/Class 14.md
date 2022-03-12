Q&A:
1. 解决IPv4地址短缺的方法：
2. IPv6的地址长度：128
3. ARP协议的主要目的是什么：逻辑地址和物理地址的转发
4. OSPF采用的路由原理：基于链路状态的路由
5. BGP是解决什么的路由问题
6. 域内路由和域间路由相同吗？不同


### Desired Bandwidth Allocation 理解 主要看上一个图
- Bandwidth levels should converge quickly when traffic patterns change

### Regulating the Sending Rate
- Slow down at the sender side for different reasons
	- Flow control
	- Congestion拥塞

### Regulating the Sending Rate !!!!!!
- Different signals of congestion that the network may use to tell the transport endpoint to slow down or speed up 

### Regulating the Sending Rate
[课本链接](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67)

- AIMD(Additive Increase Mulyiplicative Decrease)
Control law does converge to a fair and efficient point
过线前用加法 过线后用乘法 逐步快速收敛


传输层前三部分完成

---

## UDP
User Datagram Protocol is a shim over IP
- Header contains ports(TSAPs),length and checksum
- udp是无连接的 不保证可靠性

- Real Time Transport
	- RTP provides supports for sending real-time data over UDP

RIP协议就在用UDP来不断交换端口号

## Internet Transport Protocols---TCP
### The TCP service model
- TCP provides applications with a reliable byte stream between processes 可靠的字节流

### TCP Segment Header

### TCP Connection Establishment
- TCP sets up connnections with three-way handshaking
	- Release is symmetric 

### Connection Release



