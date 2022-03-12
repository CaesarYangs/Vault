# Class 16

## Q&As
1. 确认时钟的作用是什么？ P442
2. 什么是拥塞窗口 它的作用是什么？ P436
3. 在发送数据的时候是根据拥塞窗口还是流量窗口来控制发送？ 两个窗口中较小的
4. 在发送数据包的时候，满启动和线性增长的区别是什么？ 速度不同
5. 什么是快速重传和快速恢复？P445
6. 解释P445 图6-46的理解
7. 解释P446 图6-47的理解


# Application Layer
- DNS-Domain Name System
- World Wide Web
- Content delivery 

To use transport services to build distributed applications

## DNS Domain Name System
- DNS resolves high-level human readable names to low-level IP address for network hosts
	- The DNS name space
	- Resources
	- Name servers

### DNS Name Space
- DNS namespace is organized in a hierarchical manner from the root down
	- Different parts delegated to different organizations

### Resources Records
- The key resource records in the namespace are IP address and name servers,there are others too.

### Name Servers
- Name servers contain data for portions of the name space called zones
- DNS Protocal
	- Ryan on UDP port 53
	- Retransmit lost messages


P479 递归查询 迭代查询

本地域名服务器在做递归查询的操作——通过每一个.后面的根域名向每一个部分的服务器发出查询请求

根域名服务器做迭代查询——仅需要找到存储的相应一个根域名的ip信息并返回





### Content Delievery
- CDN
- BT



20个判断题 x2
名词解释 
分析（简答题）
计算