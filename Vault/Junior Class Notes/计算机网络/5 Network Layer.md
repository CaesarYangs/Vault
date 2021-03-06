# NetWork Layer
# 网络层（IP层）
## [引言](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=287)

-   网络层关注的是如何将源端数据包一路送到接收方.
    
-   为了将数据包送到接收方，可能 沿途要经过许多跳( hop)中间路由器。这种功能显然与数据链路层的功能不同，数据链路 层的目标没那么宏伟，只是将帧从线路一边传送到另 一边。因此 ， 网络层是处理端到端数 据传输的最底层。
    
-   为了实现这个目标 ， 网络层必须知道网络拓扑结构〈即所有路由器和链路的集合〉，并 从中选择出适当的路径，即使是大型网络也要选出 一条好路经。同时，网络层还必须仔细 选择路由器，避免某些通信线路和路由器负载过重，而其他线路和路由器空闲。

### [5.1.1 存储转发数据包交换](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=288)
定义：
-   在该数据包到达路由器，并且路由器的链路层完成了对它校验和的验证之后，它先 被存储在路由器上:然后沿着路径被转发到下一个路由器，直至到达目标主机，这里就是 数据包的目的地。这种机制即为存储.转发数据包交换，正如在前面几章已经看到的那样。
    
	
### [5.1.2 提供给传输层的服务](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=288)
-   网络层通过网络层/传输层接口向传输层提供服务。一个重要的问题是明确网络层向传 输层提供什么类型的服务。在设计网络层服务时，一定要牢记下面这些目标 (1 )向上提供的服务应该独立于路由器技术。 (2)应该向传输层屏蔽路由器的数量、类型和拓扑关系。 (3)传输层可用的网络地址应该有一个统一编址方案，甚至可以跨越 LAN 和 WAN

### [5.1.3 无连接服务的实现](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=289)
    
-   如果提供的是无连接的服务，那么， 所有的数据包都被独立地注入到网络中，并且每个数据包独立路由，不需要提前建立任何 设置。在这样的上下文中，数据包通常称为数据报( datagram)，它类似于电报( telegram), 对应的网络称为数据报网络( datagram network)

-   *如果使用了面向连接的服务，那么，在 发送数据包之前，必须首先建立起一条从源路由器到目标路由器之间的路径。这个连接称 为虚电路 eve, virtual circuit)，它类似于电话系统中建立的物理电路，对应的网络称为虚电路网络( virtual-circuitnetwork) .*
    
-   让我们假设在这个例子中消息的长度是最大数据包长度的 4 倍，所以，网络层必须将 消息拆分成4个数据包: 1、 ，然后用某种点到点协议(比如PPP)将这些数据包 依次发送给路由器 A
    
-   每一台路由器都有一个 内部表，它指明了针对每一个可能的目标地址应该将数据包送到哪里去。
    
-   每个表项由两部 分数据组成 z 目标地址和通往目标地址所使用的出境线路。
    
-   分别到达入境线路并且经过验证校验和之后，被路由器 暂时保存起来。然后，根据 A 上的表，每个数据包被放在一个新帧中，并且被转发到通往C 的出境链路:之后数据包 l 被转发给 E，进一步又被转发给 F。当它到达 F 时，它被封 装在一个帧内通过连有 H2 的 LAN 被发送出去。数据包 2 和 3 遵循同样的路径。

- 管理这些路由表并做出路由选择的算法称为路由算法( routing algorithm)。路由算法是我们本章学习的一个主要议题，正如我们将会看到的那样，有几种 不同类型的路由算法。

- ==IP 协议( Internet Protocol)是整个 Internet 的基础，它是无连接网络服务的重要范例。 每个数据包携带一个目标 IP地址，路由器使用该地址来单独转发每一个数据包。==

### [5.1.4 面向连接的服务的实现](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=290)
-   所有需要在这个连接上通过的流量，都 使用这条路径，这与电话系统的工作方式完全一致。当连接被释放之后，虚电路也随之消 失。在面向连接的服务中，每个数据包包含一个标识符，指明了它属于哪一条虚电路。
    
-   现在我们来考虑如果 H3 也希望与 H2 建立连接则情形会怎么样。 H3 选择连接标识符 1 (因为是它发起连接，而且这是它唯一的连接)，并且告诉网络要建立虚电路
    
-   管理这些路由表并做出路由选择的算法称为路由算法( routing algorithm)。路由算法是我们本章学习的一个主要议题，正如我们将会看到的那样，有几种 不同类型的路由算法。

-   在有些上下文中，这个过程称为标签交换( label switching)。一种面向连接的网络服务 例子是多协议标签交换( MPLS, MultiProtocol Label Switching)，它主要被用在 Internet ISP网络， IP数据包被一个有20位连接标识或标签的MPLS头包裹着。

### ==[5.1.5 虚电路与数据报网络的比较](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=291)==

-   从保证服务质量以及避免网络拥塞的角度来看，虚电路有一定的优势，因为在建立连
    
-   在网络内部，数据报和虚电路网络之间存在着几个方面的权衡。一个权衡在于建立时 间和地址解析时间。使用虚电路需要一个建立阶段，这个阶段既花费时间也消耗资源。然 而，一旦付出了这个代价，处理一个数据包的方法却非常简单:路由器只要使用电路号作 为索引，在表中找到该数据包的去向即可。在数据报网络中，不需要建立电路，但路由器 需要执行一个更为复杂的查找过程以便找到目标表项。
    
-   与此相关的问题是数据报网络所用的目标地址比虚电路网络所用的电路号要长

-  从保证服务质量以及避免网络拥塞的角度来看，虚电路有一定的优势，因为在建立连接时，资源可以提前预留(比如缓冲区空间、带宽和 CPU 周期〉。一旦数据包开始到来， 所需要的带宽和路由器容量都已经准备就绪。而对于数据报网络，避免拥塞更困难些。

-   一条通信线路的失 败对于使用了该线路的虚电路来说是致命的，但如果使用数据报，则这种失败很容易得到 弥补。数据报还允许路由器平衡网络流量，因为一个长序列数据包的传输路径可以在序列 传输的中途改变。

## [5.2 路由算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=292)
- ==选择路由 的算法以及这些算法所用的数据结构是网络层设计的最主要内容。==
    
-   路由算法 Crouting algorithm)是网络层软件的一部分，它负责确定一个入境数据包应 该被发送到哪一条输出线路上。如果网络内部使用了数据报，那么路由器必须针对每一个 到达的数据包重新选择路径
    
-   有的时候对路由和转发这两个功能进行区分是非常有用的，路由即对使用哪一条路径 做出决策，而转发则是当一个数据包到达时该采取什么动作。可以把路由器想象成内部有 两个进程。其中一个进程在每个数据包到达的时候对它进行处理，它在路由表中查找该数 据包所对应的出境线路。这个进程即为转发 Cforwarding)进程:另一个进程负责生成和更 新路由表，这正是路由算法发挥作用的地方。

 [自适应与非自适应算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=293)

-   自适应算法( adaptive algorithm)则会改变它们的路由决策以便反映出拓扑 结构的变化，通常也会反映出流量的变化情况。这些动态路由( dynamicron出g)
    
-   非自适应算法( nonadaptive algorithm)不会根据当前测量或者估计的流量和拓扑结构，来调整它们的路由决策。相反， (对所有的 J) 所使用的路由选择是预先在离线情况下计算好，并在网络启动· 时被下载到路由器中的。这个过程有时候也称为静态、路由(static routing)

### [5.2.1 优化准则](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=294)

-   作为最优化原则的一个直接结果，从所有的源到一个指定目标的最优路径的集合构成 了一棵以目标节点为根的树
    
-   ==所有路由算法的目标是为所有路由器找到这样的汇集树，并根据汇集 树来转发数据包。==

### [5.2.2 最短路径算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=295)

-   一般情况下，边上面的标记可以作为距离、带宽、平均流量、通信成本、平均延迟等 其他因素的一个函数，通过计算得出。通过改变函数的权重，路由算法就可以根据任何一 种标准或者多种标准的组合来计算“最短”路径。

### [5.2.3 泛洪算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=297)

-   在实现路由算法时，每个路由器必须根据本地知识而不是网络的全貌做决策。一个简 单的本地技术是泛洪( flooding)，这种技术将每一个入境数据包发送到除了该数据包到达 的那条线路以外的每条出境线路。

- 其次，泛洪途径的鲁棒性非常好。即使大量路由器被炸成碎片(例如，位于战争地区 的一个军事网络〉，泛洪也能找到一条路径(如果存在〉，使得数据包到达目的地。泛洪需 要的安装很少，路由器仅仅需要知道自己的邻居即可。这意味着，泛洪可以作为其他路由 算法的基本构件，那些算法更有效但需要更多的处理。泛洪还可用作其他路由算法进行比 较的性能度量。因为泛洪能并发选择每一条可能的路径，因此总能选出最短的那条路径， 没有其他算法能够产生一个更短的延迟(如果我们忽略泛洪过程本身产生的开销〉。

### ==[5.2.4 距离矢量算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=298)==
-   计算机网络通常使用动态路由算法。
    
-   ==距离矢量路由( distance vector routing)算法是这样工作的：每个路由器维护一张表(即 一个矢量〉，表中列出了当前己知的到每个目标的最佳距离，以及所使用的链路。这些表通过 邻居之间相互交换信息而不断被更新，最终每个路由器都了解到达每个目的地的最佳链路。==
    
-   在距离矢量路由算法中，每个路由器维护一张路由表，它以网络每个路由器为索引， 并且每个路由器对应一个表项。该表项包含两部分:到达该目标路由器的首选出境线路， 以及到达该目标路由器的距离估计值。距离的度量可能是跳数，或者其他因素，正如我们 在计算最短路径时讨论的那样。
    
-   假定路由器知道它到每一个邻居的“距离”。如果所用的度量是跳数，那么该距离就是 跳。如果度量值为传播延迟，则路由器很容易测量出链路的传播延迟。它只要直接发送 一个特殊的 ECHO 数据包给邻居，邻居收到后盖上时间戳，尽可能快地发回来即可。

[距离矢量算法中的无穷计算问题](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=299)

-   整个网络最佳路径的寻找过程称为收敛( convergence)。距离矢量路由算法作为 一 项简 单技术很有用，因为路由器可以在所有路径中有选择地计算出一条最短路径。但实际 有一个严重的缺陷:虽然它总是能够收敛到正确的答案，但速度可能非常慢。

### ==[5.2.5 链路状态路由](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=301)==
    
-   链路状态路由算法的设计思想非常简单，可以用五个部分加以描述。每一个路由器必 须完成以下的事情，算法才能正常工作: 
1. 发现它的邻居节点，并了解其网络地址。 
2. 设置到每个邻居节点的距离或者成本度量值。 
3. 构造一个包含所有刚刚获知的链路信息包。 
4. 将这个包发送给所有其他的路由器，并接收来自所有其他路由器的信息包。 
5. 计算出到每个其他路由器的最短路径。
    
-   1979 年以前 ARPANET 一直使用距离矢量路由算法，而在此之后则改为使用链路状态 路由算法。导致距离适量算法退位的主要问题在于，当网络拓扑结构发生变化后距离矢量 路由算法需要太长时间才能收敛到稳定状态(由于无穷计数问题)。因此，距离矢量路由算 法被一个全新的算法所替代，该算法称为链路状态路由算法( link state routing)。
    
-   ==实际上，算法将完整的拓扑结构分发给了每一个路由器。然后每个路由器运行 Dijkstra 算法就可以找出从本地到每一个其他路由器的最短路径。==
    
-   **发现邻居**
-   当一个路由器启动时，它的第一个任务是找出哪些路由器是它的邻居。为了实现这个 目标，它只需在每一条点到点线路上发送一个特殊的 HELLO 数据包。线路另一端的路由 器应该返回一个应答说明自己是谁。这些名字必须是全局唯一的

- **设置链路成本**
- 为了寻找最短路径，链路状态路由算法需要每条链路以距离或成本度量。

- **构造链路状态包**
- 一旦收集到了所需要的交换信息，每个路由器的下一步工作是构建一个包含所有这些 信息的数据包。该数据包的内容首先是发送方的标识符，接着是一个序号( Seq)和年龄 (Age，后面再介绍)，以及一个邻居列表。

- **分发链路状态包**
链路状态路由算法最技巧的部分在于分发链路状态数据包。所有路由器必须快速并可 靠地获得全部的链路状态数据包。如果不同的路由器使用了不同版本的拓扑结构，那么它 们计算出来的路由可能会不一致，例如出现环路、目标机器不可达以及其他的问题。

      
[链路状态算法实例-表格图eg](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=303)
- 发送标志表明该数据包必须在所指示的线路上发送。确认标志 表明它必须在这条线路上得到确认。

- [**计算新路由 **](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=304)

-   一旦路由器己经积累了全部的链路状态数据包之后，它就可以构造出完整的网络图， 因为每条链路都己经被表示出来了。事实上，每条链路被表示了两次，每个方向各表示一 次。不同方向的链路可能有不同的成本。最短路径计算可找到从 与从 不同 的路径。
    
-   现在可以在路由器本地运行 Dijkstra 算法，以便构建出从本地出发到所有可能目标的 最短路径。这个算法的运行结果告诉路由器到达每个目的地能够走哪条链路。这个信息被 安装在路由表中，而且恢复正常操作。
    
-   ==相比距离矢量算法，链路状态路由算法需要更多的内存和计算。对于一个具有 n 个路 由器的网络，每个路由器有 k个邻居，那么，用于存储输入数据所要求的内存与 h 成正比， 这至少与列出全部目的地的路由表一样大。而且，计算时间的增长快过 h ，即使采用最有 效的数据结构，在大型网络中运行这个算法依然是个问题。不过，在许多实际场合，链路 状态路由算法工作得很好，因为它没有慢收敛问题。==

### *[5.2.6 层次路由](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=305)*
    
-   在采用了分层路由之后，路由器被划分成区域( region)。每个路由器知道如何将数据 包路由到自己所在区域内的目标地址，但是对于其他区域的内部结构毫不知情。当不同的 网络被相互连接在一起，很自然地就会将每个网络当作一个独立的区域，一个网络中的路 由器不必知道其他网络的拓扑结构。

## [5.3 网络层-拥塞控制算法](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=315)
-   传输层共同努力协同工作。 数据包。然而，控制拥塞的最有效方法是减少传输层注入网络的负载。这就需要网络层和 拥塞发生在网络内，正是网络层直接经历着拥塞，而且必须由它最终确定如何处理过载的 能，这种情况称为拥塞( congestion)。网络层和传输层共同承担着处理拥塞的责任。由于 (一部分)网络中存在太多的数据包导致数据包被延迟延迟和丢失，从而降低了传输’性
    
-   网络层和传输层共同承担着处理拥塞的责任 #计算机网络考点 
    
-   ==然而，控制拥塞的最有效方法是减少传输层注入网络的负载。这就需要网络层和 传输层共同努力协同工作。==

### [5.3.1 拥塞控制途径](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=317)

-   拥塞的出现意味着负载(暂时)大于资源(在网络的一部分〉可以处理的能力。很自 然人们能想到两个解决方案:增加资源或减少负载。
    
-   这称为流量感知的路由(traffic-aware routing)。把流量拆分到多个路径也是有 用的。
    
-   然而，有的时候不可能增加容量。那么对抗拥塞的唯一 的办法就是降低负载。在 虚电路网络中，如果新的连接将导致网络变得拥挤不堪，那么就应该拒绝这种新连接的建 立。这种控制称为准入控制( admissioncontrol)

[显示拥塞控制](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=321)

-   显式拥塞通知 除了生成额外的包发出拥塞警告外，路由器可以在它转发的任何数据包上打上标记(设 置数据包头的某一个标志位)发出信号，表明它正在经历着拥塞。当网络传递数据包时， 接收方可以注意到有个拥塞己经发生，在它发送应答包时顺便告知发送方。然后发送方可 以像以前那样紧急刹车降低传输速率。

### [5.5.3 隧道](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=343)
    
-   这个问题的解决方案是一种称为隧道(阳nneling)的技术。为了给伦敦办事处的主机 发送一个 IP 数据包，巴黎的主机构造一个包含伦敦 1Pv6 地址的数据包，然后将该数据包 发送到连接巴黎 1Pv6 网络到 IPv4Internet上的多协议路由器:


 ### [互联网路由](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=345)

所有这些因素导致了两级路由算法。在每个网络中，使用一个域内( intradomain)或者内部网关协议( interiorgateway protocol)进行路由(“网关”是“路由器”的旧称)。这 可能是我们己经描述过的一种链路状态协议。为了让数据包跨越构成互联网的网络，就需 要用到域间( interdomain)或外部网关协议( exterior gateway protocol)。网络可能全部使 用不同的域内协议，但它们必须使用相同的域间协议。在 Internet 上，域间路由协议称为 边界网关协议( BGP , Border Gaterway Protocol)

### [ 5.5.5 数据包分段](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=345)

 [透明分段与非透明分段](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=346)

-   将分段重新组成原始的数据包，可以采用两种对立的策略。第一种策略，由“小数据 包”网络引起的分段过程对于沿途后续的网络都是透明的，也就是说，从该网络一直到最 终的目标途中的每个网络都感觉不到曾经发生过分段，
    
-   透明的分段过程非常直接、简单，但是也有一些问题。首先，出口路由器必须知道什 么时候它己经接收到了全部的段，所以每个分段中必须提供一个计数字段或者一个“数据 包结束”标志位。其次，由于所有的数据包必须经过同一个出口路由器才能进行重组，因 此路由受到了限制。由于不允许有些段沿着一条路径到达最终目标，而另一些段沿着一条 不相交路径到达最终目标，所以，可能会损失一些性能。更为重要的是，路由器可能不得 不做大量的工作。如果不是所有的段都己到达，它还需要缓冲到达的段，并且决定何时丢 弃这些段。某些工作可能纯粹是一种浪费，因为当一个数据包需要通过一系列的小数据包 网络时，需要多次被分段和重组。
    
-   另一种分段策略是避免在任何一个中间路由器上重新组合分段。

[Page 334](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=347)

-   则每个段都被当作原始的数据包一样来对待。 路由器传递这些段的情形 542 Cb)所示，重组过程只在目标主机上进行。
    
-   非透明分段的主要优点是路由器所做的工作比较少。 IP 就是以这种方式工作的。 完整的设计要求分段以可以重新构建原有数据流的方式编号。 IP 采用的设计思想是:给每 个段一个数据包序号〈所有的数据包都携带〉、 一个数据包内的绝对字节偏移量和一个指明 是否到达数据包末尾的标志位。

## [5.6 Internet 的网络层](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=348)

-   现在，让我们离开通用设计原则，开始 Internet 网络的探索之旅。在网络层，可以把 Internet看作是一种相互关联的网络或自治域(自治系统)集合。没有真正的结构，但存在 几个主要骨干网。这些都是由高带宽线路和快速路由器组成。这些骨干网中最大的一个称 为一级网络( Tier 1 networks )，每个骨干网都与它连接，进而到达其他骨干网。连接到骨 干网上的是 Internet 服务提供商 CISP, Internet Service Provider)，它为家庭和企业、数据 中心和服务器托管设施，以及区域(中级)网络提供 Internet 接入服务

### [5.6.1 1Pv4 协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=350)

-   区分服务 CDifferentiated services)宇段是少数几个在意义上随岁月(轻微)改变的宇 段之一。
    
-   总长度 CTotal Jen酬。宇段包含了该数据报中的所有内容，即头和数据。最大长度是 65 535个字节。
    
-   标识 Cldentification)宇段的用途是让目标主机确定一个新到达的分段属于哪一个数据 报。
    
-   接下来的两个 I 位宇段与分段有关。 DF 代表“不分段”( Don’tFragment)标志位。这 是针对路由器的一条命令，它不允许路由器分割该数据报。
    
-   MF 代表“更多的段”( More Fragment~)标志位。除了最后一个段以外，其他所有的 段都必须设置这一位。
    
-   分段偏移量( Fragment et)宇段指明了该段在当前数据报中的位置。除了数据报的 最后一个段以外，其他所有段的长度必须是 8 字节的倍数
    
-   生存期(Time to live)宇段是一个用于限制数据包生存期的计数器。

[严格与松散路由](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=352)

-   严格源路由( Strict source routing)选项给出了从源到目标的完整路径，其形式是一系 IP 地址。
    
-   松散源路由( Loose source routing)选项要求该数据包穿越所指定的路由器列表，并且 要求按照列表中的顺序前进:但是，在途中也允许经过其他路由器。通常情况下，该选项 往往只提供少数几个路由器，用来强迫数据包走一条特殊的路径。例如，为了强迫一个从 伦敦到悉尼的数据包必须向西走而不是向东走，该选项可以指定纽约、洛杉矶和檀香山的 路由器作为路由必经节点。当出于政治或者经济的考虑而要求经过或者避开某些国家的时 候，这个选项最有用。

### [5.6.2 IP地址](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=353)
    
-   前缀 与以太网地址不同的是 IP 地址具有层次性。每个 32 位地址由高位的可变长网络和低 位的主机两部分数据组成。
    
-   地址的书写方式是点分十进制表示法。按此格式， 4 个字节中的每个写成十进制， 取值范围从 255c.
    
-   以这种格式书写时称为子网掩码(subnet )，它可以与一个 IP地址进 AND 操作，以便提取出该 E 地址的网络部分。在我们的例子中，子网掩码为 255.255.255.0。图 5-48 显示了 一个前缀和一个子网掩码。

### [子网](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=354)

-   为了避免冲突，网络地址的管理由一个称为 Internet 域名和地址分配机构 CICANN, Internet Corporation for Assigned Names and Number)的非营利性公司负责。 ICANN 一次把 部分地址空间授权给各区域机构，这些机构再把 IP 地址发放给 ISP 和其他公司。这就是一 家公司获得一块田地址的过程。
    
-   问题的解决方案是，在内部将一个网络块分成几个部分供多个内部网络使用，但对外 部世界仍然像单个网络一样。这就是所谓的子网划分( subnetting)，分割一个大型网络得 到的一系列结果网络(比如以太网〉称为子网( subnet)。正如我们在第 1 章中提到的那样， 你应该意识到这个词的新用法和旧的用法有冲突，子网的以前含义是指网络中的所有路由 器和通信线路的集合。

[子网部分继续](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=355)

-   当数据包到达时，路由器会查看该数据包的目标地址，井检查它属于哪个子网。具体 做法是:路由器把数据包的目标地址与每个子网的掩码进行 AND 操作，看结果是否对应 于某个前缀。
    
### [CIDR一一无类域间路由](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=356)

-   有了地址聚合， IP地址可包含大小不等的前缀。同样一个IP地址，一台路由器把它当 作/22 的一部分对待(该地址块包含 210个地址)，而另一台路由器把它当作一个更大的120 一部分对待(其中包含 212个地址)。这是因为每个路由器有相应的前缀信息。这个设计和 子网划分协同工作，统称为无类域间路由( CIDR, Classless Inter-Domain Routing)，发音 为“ cider”。它的最新版本由 RFC 4632 说明( Fuller 和 Li, 2006 年)。这个名字突出了与 有类别的地址层次编码的不同，稍后我们将简要介绍这点。
    
-   幸运的是，我们可以做一些事情来减小路由表的长度。我们可以运用与子网划分相同 的观点 z 不同地点的路由器可以知道一个给定 IP 地址的不同大小前缀。然而，不是将一块 地址分割成子网，相反，在这里我们把多个小前缀的地址块合并成一个大前缀的地址块。 这个合并过程称为路由聚合( route aggregation)，由此产生的较大前缀地址块有时称为超网 Csupernet)，以便有别于地址块的分割。

[域间路由前缀](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=357)

-   当聚合功能被启用后，这个过程完全自动。这依赖于给 Internet 分配什么样的前缀， 而不是给网络分配地址的管理员行动。聚合技术在 Internet 中被大量使用，已经把路由器 表的大小减少到目前的约 200 000 万前缀。
    
-   更为扭曲的是前缀允许重叠。规则是数据包按最具体路由的方向发送，即具有最少 IP 地址的最长匹配前缀(longestmatchingprefix )。最长匹配前缀路由提供了有益的灵.活性， 正如从图 5-52 显示的纽约路由器的行为。该路由器仍使用单一聚合前缀把三所大学的流量 发送到伦敦。然而，该前缀中的先前那块未用地址现在已经分配给了旧金山的网络。一种 可能是纽约路由器保持四个前缀，其中三个前缀的数据包发送到伦敦，第四个前缀的数据 包发送到旧金山。相反，最长匹配前缀路由可以用图中显示的两个前缀来转发。一个总的 前缀指示把整个地址块的流量发到伦敦:一个更具体的前缀用来指示该大前缀的一部分流 量发往旧金山。有了最长匹配前缀规则，到旧金山网络的 IP 地址的流量将被发送到通往旧 金山的出境线路，并且发往大前缀中所有其他 E 地址的流量将被送往伦敦。

[分类和特殊寻址](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=358)

-    为了帮助你更好地理解为什么 CIDR 如此有用，我们简要介绍之前的地址设计方案。 1993年以前，E 地址被分为图 5-53列出的 5个类别。这种分配己经称为分类寻址( classful addressing)

[NAT-网络地址转换](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=360)
    
-   这种匮乏导致了一些保守使用 IP地址的技术。其中一种方法是为一台连在网上并使用 网络的计算机动态分配一个 IP 地址，而且在该主机不活跃时收回分配给它的 IP 地址:
    
-   IP 地址非常匮乏

### [IPv6](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=363)

-   在本节，我们将介绍两个问题，并提出若干解决方案。唯一的长期解决方案是移动到 更大的地址空间。 1Pv6 CIP 版本 6)就是能做到这点的一个替换设计。它采用 128 位地址， 在可预见的将来任何时间都不可能出现地址短缺这个问题。

### [Internet控制协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=370)

-   除了用于数据传输的 IP 协议外， Internet 在网络层还有几个辅助控制协议。它们包括 ICMP 协议、 ARP 协议和 DHCP 协议。

[ICMP-一-Internet 控制消息协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=371)
    
-   路由器严密监视 Internet 的操作。当路由器在处理一个数据包的过程中发生了意外， 可通过 Internet控制消息协议。CMP, Internet Control Message Protocol)向数据包的源 报告有关事件: ICMP 还可以用来测试 Internet。

[ARP-一一地址解析协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=372)
    
-   现在问题来了 z 如何将 IP 地址映射到数据链路层的地址，比如以太网地址呢?
-   与采用配置文件相比，使用 ARP 协议的优点是简单。系统管理员只要给每台机器分配 一个IP地址，并且确定好子网掩码，不用做其他任何事情。 ARP会负责处理好所有其他的 事情。

-   我们观察到出现在每个网络上的帧的以太网地址发生 了改变，而 IP地址保持不变(因为它们表示所有互联网络的端点)。

[DHCP-动态主机配置协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=374)

-   我们观察到出现在每个网络上的帧的以太网地址发生 了改变，而 IP地址保持不变(因为它们表示所有互联网络的端点)。

-   ARP C以及其他 Internet协议)都做了这样的假设，即主机配置了一些基本信息，比如 自己的 IP 地址。主机如何获得此信息?手动配置每台计算机是可能的，但那既乏味又容易 出错。有一个更好的方法可以完成这件事情，就是动态主机配置协议 CDHCP, Dynamic Host Configuration Protocol)。

### [5.6.6 OSPF一一内部网关路由协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=377)

[Page 365](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=378)

-   Cin位adomain routing) 部，一个组织可以使用自己的内部路由算法，或者更流行的名称叫域内路由算法 System)构成，并由不同的组织运营，这些组织通常是公司、大学或 ISP。在自己网络内 正如我们前面提到的， Internet 由大量的独立网络或自治系统( AS, Autonomous
    
-   为内部网关协议(interior gateway protocol)。
    
-   在下一节，我们将探讨独立运营网络之间的 路由问题，或域间路由( interdomain routing)问题。在这种情况下，所有网络必须使用相 同的域间路由协议和外部网关协议( exteriorgateway protocol)。 Internet 采用的域间路由协 议是边界网关协议( BGP, Border Gateway Protocol)。
    
-   路由信息协议(阳P, Routing Information Protocol)是当时运行的 一个主要例子。在小型网络系统中阳P 运作良好，但随着网络规模变得越来越大它工作得 就不那么好了:而且它还遭受无穷计数问题的困扰，收敛速度一般很慢。
    
-   1988 年 IEπ 开始为域内路由设计一个 链路状态路由协议。该协议在 1990 年成为标准，它就是开放最短路径优先 COSPF, Open Shortest Path First)。

[OSPF的工作机制](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=379)

-   OSPF 的工作方式本质上是对一张图进行操作:将一组实际网络、路由器和线路抽象 到一个有向图中，图中的每条弧有一个权值(距离、延迟等)
    
-   OSPF 协议从根本上做了两 件事情，首先用一个类似这样的图来表示实际的网络，然后每个路由器使用链路状态方法 计算从自身出发到所有其他节点的最短路径。
    
-   有可能协议会发现多个同样短的路径，在这 种情况下， OSPF 记住最短路径集合，并在报文转发期间把流量分摊到这些路径上。这种 多路径路由方法有助于负载均衡。该方法称为等价成本多路径

### [BGP一一外部网关路由协议](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=382)

-   在一个 AS 内部，推荐使用的路由协议是 OSPF 和 IS-IS。在 AS 之间，则可以使用另 一个协议，称为边界网关协议( BGP, Border Gateway Protocol)。
    
-   之所以在 AS 之间需要一 个完全不同的协议，是因为域内协议和域间协议的目标不同。域内协议所需要做的只是尽 可能有效地将数据包从源端传送到接收方，它不必考虑政治方面的因素

[Page 370](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=383)

-   这一政策称为对等( peering)传输。
    
-   BGP 是距离矢量协议的一种形式，但它与域内距离矢量协议〈比如 RIP)有很大的不
    

[Page 371](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=384)

-   我们己经看到用政策而不是最小距离来选择使用哪些路由。另一个很大的区别是， BGP 不仅维护到每个目的地的成本，而且每个 BGP 路由器还跟踪所使用的路径。这种方法称为 路径矢量协议( path vector protocol)



## [小结](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=389)

-   网络层向传输层提供服务，它既可以基于虚电路，也可以基于数据报。在这两种情形 下，它的主要任务是将数据包从源端路由到接收方。在数据报网络中，路由决策针对每 个数据包而作;在虚电路网络中，路由决策在建立虚电路时做出。
    
-   计算机网络用到了许多路由算法。泛洪是最简单的算法，它把数据包发送到所有的路 径上。大多数算法寻找一条最短路径，井能自适应网络拓扑的变化 。 主要的算法是距离矢 量算法和链路状态算法。大多数网络实际使用了其中的某一个算法。其他重要的路由话题 包括大型网络的层次路由、移动主机的路由、广播路由、组播路由和选播路由。
    
-   网络很容易变得拥塞，从而增加了数据包延迟和丢失。网络设计者企图通过一系列手 段来避免拥塞，其中包括设计具有足够容量的网络、选择未拥堵的路由、拒绝接受更多的 流量、给源端发信号降低速度以及负载脱落。

-   的网络具有不同的最大数据包长度时，可能需要分段。不同网络内部可运行不同的路由协 议，但外部必须运行公共的路由协议。有的时候，隧道一个数据包穿越一个敌对网络能解 决问题，但是，如果源网络和目标网络的类型不同，这种方法就会失败。
    
-   Internet 的网络层有丰富多样的协议。这些协议包括数据报协议 IP 和控制相关协议， 比如 ICMP, ARP 和 DHCP。一个称为 MPLS 的面向连接协议携带 IP 数据包穿过某些网络。 网络中使用的主要路由协议是 OSPF，穿越网络用的路由协议是 BGPo Internet正快速消耗 IP 地址，所以 IPv6 作为 IP 的新版本己经开发出来，并正在被如此之慢地部署着。