主要考察风格：
管道
N 层
MVC
BS
CS

之前的那些组件按照什么方式来组织

- 什么是设计模式和设计风格
- 经典软件设计风格：mvc n 层 管道 基于消息处理机制 分布式 面向服务 

软件设计内容维度：
- 层次化表达
- 抽象和信息隐藏
- 分而治之 精细化方法

连接件就是将识别出来的组件进行如何交互和连接

- 基本连接机制
	- 层次化表达机制
	- 包含
	- 依赖
	- 关联
	- 调用
	- 共享
- 复杂连接机制
	- 客户端 服务端协议
	- 连接数据库
	- 非同步广播
	- 管道数据流


1. 什么是设计风格及其重要性
2. 掌握经典的设计风格
3. 在设计的过程中能会使用这样的架构

*什么是设计风格*
是一种体系架构
- 对重复出现的重复问题的解决方法论 是最佳实践
- 提供了设计的经验 能够重用
- 实现不同层级的抽象
- 采用通用标准化的词汇来进行人员间的交流
- 进行文本化 更好地构建设计文档
- 能够预先将要定义的要素预设到系统中

管道设计风格
过滤器
数据流模式-特殊的管道设计风格

n 层
将组件分为若干个类型
实现图形层与用户层 用户层与业务逻辑层 业务逻辑层与数据访问层的分离
最典型的分布式结构程序设计


## 管道设计风格
- 软件架构中反复出现的一种基本风格是管道架构（也称为管道和过滤器架构）。一旦开发人员和架构师决定将功能拆分为独立的部分，这种模式就随之而来了。大多数开发人员都知道这种架构是Unix终端shell语言（如Bash和Zsh）背后的基本原理。
- 许多函数式编程语言的开发人员将看到语言构造和这种架构元素之间的相似之处。实际上，许多使用MapReduce编程模型的工具都遵循这个基本拓扑结构。虽然这些示例展示了管道架构风格的底层实现，但它也可以用于更高级别的业务应用。
- 管道和过滤器以特定的方式协调，管道通常以点对点的方式在过滤器之间形成单向通信。


[第11章 管道架构风格 - 简书](https://www.jianshu.com/p/3842a4183fd1)


