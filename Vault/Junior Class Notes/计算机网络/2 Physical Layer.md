# Physical Layer
## [2.5.3 频分复用](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=116)

-   因此，人们研究出复用模式使多个信号共享传输线路。

[频分复用详解](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=117)

-   频分复用 CFDM, Frequency Division Multiplexing)利用通带传输的优势使多个用户共 享一个信道。它将频谱分成儿个频段，每个用户完全拥有其中的一个频段来发送自己的信 号。
    
-   比语音通信所需多出来的那部分频带称为保护带(guard band)，它使信道之间完全隔离。采用频分多路复用时，首先，每个语音信道的频率得到不 同程度的提升:然后，把它们合并在一起。

## [2.5.4 时分复用](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=118)

-   相对频分复用的另一种复用方法是时分多路复用(TDM, TimeDivisionMultiplexing)。 在这种方式下，用户以循环的方式轮流工作。
    
-   间槽( time slot)取出并输出到混合流。
    
-   方式要求输入流在时间上必须同步。类似于频率保护带，为了适应时钟的微小变化可能要 增加保护时间( guardtime )间隔。

## [2.5.5 码分复用与码分多址](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=119)

-   码分复用( CDM, Code Division Multiplexing)是扩展频谱( spread spectrum)通信的一种形式，它把一个窄 带信号扩展到一个很宽的频带上。这种方法更能容忍干扰，而且允许来自不同用户的多个 信号共享相同的频带。由于码分复用技术最常用于第 二个目的，因此它称为码分多址

    
> CDMA 允许每个站利用整个频段发送信号，而且没有任何时间限制。利用编码理论可 以将多个并发的传输分离开。 CDMA不再假设冲突的帧被完全丢弃掉。相反，它假设多个 信号可以线性叠加。在讨论具体算法之前，我们来看一个类似的场景:在一个机场候机大 厅里，许多人正在两两交谈。 TDM 可以看作是所有的人都聚集在大厅里按顺序进行交谈。

> FDM 可以看作是大厅里的人以不同的语调交谈，某些语调高些，某些语调低些，所有的交

> 谈可同时进行并相互独立。 CDMA可以看作是大厅里的每一对交谈使用不同的语言。讲法 语的这一对在谈论有关法国的事情，并且把所有与法国无关的内容都当作噪声拒绝掉。因 此， CDMA 的关键在于 1 能够提取出期望的信号，同时拒绝所有其他的信号，并把这些信 号当作噪声。下面简单描述 CDMA 的工作原理。

## [电路交换](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=138)

## [包交换](x-devonthink-item://FB62D424-1B13-4740-A33F-51B1C18AEF67?page=140)

-   包交换 替代电路交换的一个方案是包交换，如图 2-43 (b)所示，第 1 章对此已经有所描述。 有了这项技术，数据包尽可能快地被发出，这里无须像电路交换那样要事先设立一条专门 的路径。
    
-   而在数据包交换中， 没有固定的路径，不同的数据包可以走不同的路径，路经的选择取决于它们被传输时的网 络状况，所以它们到达接收端的秩序可能出现混配。
    
-   因为在数据包交换中没有为传输数据预留 带宽，数据包可能不得不等待一段时间才能被转发。这样就引入了排队延迟( queuing delay)，如果许多包要在同一时间被发送出去还会引入拥塞。