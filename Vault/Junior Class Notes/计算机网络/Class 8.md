## Pre：Q&As
Q2: ARQ解释
Q3:
Q4:什么是滑动窗口 发送端与接收端
Q5:什么是
Q5:如何实现go back n---管道


# Chapter4 Medium Access Control Sublayer-介质访问控制子层
——MAC子层
介质访问控制子层 解决同时发送的冲突问题
在共享介质之下发送数据，有一种协议来种菜共享控制信道问题
**目的解决问题：广播网络中的多方竞争信道使用权以及分配问题**

The MAC sublayer
- Responsible for deciding who sends next on a multi-access link
an import part of the layer, *especiallly for LANs*  #计算机网络考点 LAN是什么 especially？
> Local Area Network 局域网

MAC层位于数据链路层底部——Link #计算机网络考点 
Q：为什么在底部？ A：数据链路层是完成两点之间数据可靠传送的 首先要抓住信道才能开始后面的传送
mac层的概述
mac层的位置
mac层对那些网络适用

## Chanel Allocation Problem-信道分配问题
- Fixed channel, traffic from multiple users-静态信道分配
	- Divide up bandwidth using FTM,TDM,CDMA
	- A static allocation  e.g. FM radio
	**Static allocation performs poorly for bursty traffic**
	- Allocation to a user sometimes goes unused

	> 既然所有的传统静态信道分配方法都不适应突发性的流量,我们现在就来研究动态的信道分配方法。

- Dynamic allocation assigns the channel to a user the user needs it 需要的时候给 不需要不给 动态信道分配
	- Potentially N times as efficient for N users

1. Independent traffic流量独立
often not a good model, but permits analysis 
该模型是由N个独立的站(比如计算机、电话)组成的,每个站都有一个程序或者用户产生要传输的帧。
2. Single traffic
no external way to coordinate senders
所有的通信都用这一个信道。所有的站可以在该信道上传输数据,也可以从该信道接收数据。所有站的能力都相同,尽管协议可能为站分配不同的角色(比如,优先级)。
3. Observable collisions
needed for liability; mechanisms vary 
当观察到冲突的帧后便可以再次发送冲突点位的帧
4. Continuous or slotted time
spotting may improve performance
把时间分配成连续的时间槽 帧传输只能从某个时间槽的起点开始。
5. **Carrier sense载波监听**
can improve performance if available
一个站在试图用信道之前就能知道该信道当前是否正被使用。

## Multiple Access Protocols-多路访问协议
### ALOHA
#### 纯ALOHA
时间是连续的
- In pure ALOHA, users transmit frames whenever they have data
	- Users retry after a **random** amount of time for collisions 错峰发送
- Efficient and low delay in low load environment
- 冲突在其他用户同时发送的时候出现
#还不太明白 

#### 分槽ALOHA
时间被分成了若干时间槽 每个时间槽对应一帧
- Slotted ALOHA is twice as efficient as pure ALOHA
	- Low load wastes slots, high loads causes collisions
	分时序发送的ALOHA效率更高
	不可以在任意时刻发送 有固定的时间流
	连续的纯ALOHA变成了离散的ALOHA，这将容易受冲突期减少了一半

### CSMA (Carrier Sense Multiple Access) 载波监听多路访问协议
- CSMA improves on ALOHA by sensing the channel 
	- User doesn't send if it senses someone else is sending
- Variations on what to do if the channel is busy
	- 1-persistent sends as soon as the channel becomes idle
	- Non-persistent waits for a random amount of time before trying again
	- p-persistent sends with proximity p when idle 
**根本问题在于如何减少冲突** 错开包和信息的发送时间

#### 1-Persistent CSMA 1-坚持
传输的概率为1
会持续对目标信道进行载波监听
当发现信道空域后，一定会立即进行传输

#### Nonpersistent CSMA 非坚持
等待时不对信道进行连续监听。等待一段随机事件，然后再次进行监听。
算法带来了更好的信道利用率，但也带来了更大的延迟

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



