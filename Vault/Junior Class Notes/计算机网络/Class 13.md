- Q&As
1. 计算机网络的哪些层次负责处理拥塞控制
网络层整个和传输层
2. 拥塞控制最有效果的方法
减少传输层注入的负载
为什么是减少传输层 而不是应用层？——网络层的上方是传输层
3. 列举拥塞控制的技术途径
4. 数据包分段的那几种类型
因特网IP层采用非透明
5. IP地址哪两部分组成
网络号主机号
什么是子网掩码？


### 续 子网

子网将ip的不同部分或者叫前缀分开 方便更好的管理
内部二级路由
对外简洁好管理


子网实际上是占用了B类地址主机的空间 抽取一部分来作为子网号

为了管理可以从主机号里面提取一部分位数作为子网号

### NAT Network Address Translatation 网络地址转换——了解
实际上是解决IP地址短缺与匮乏的技术方案

CIDR也是解决IP匮乏的方案

### IPv6 ——了解
产生主要是为了解决地址短缺的问题

### Internet Control Protocols Internet控制协议
**ICMP**了解
**ARP——地址解析协议**
- Let nodes find target Ethernet addresses from their IP address 

IP地址 逻辑地址 物理地址 MAC地址 转换

Bridge和Switch是为了扩展局域网
扩展更多的网络用Router

**DHCP——动态主机的分配**了解
解决IP短缺的方法之一

### OSPF 内部网关路由协议——域内路由
OSPF主要基于链路状态 是因特网广泛使用的传输协议

RIP基于距离矢量

标准存在的意义：为了互通有无 互联互通

### BGP——域间路由
是基于距离矢量



## 6 传输层
重点：
- Congestion Control
- UDP
- TCP


### Service Protocal to the Upper Layers
- Add reliable to the network layer
- 传输层真正联系了上层应用
- 一个是传输层地址 一个是网络层地址

IP地址是用来进行机器的寻址



