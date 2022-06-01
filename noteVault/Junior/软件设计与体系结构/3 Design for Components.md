
==**软件体系结构实际上就是对组件和连接机制 对待构建系统 做工程上的表达**==

利用中间件的软件组件设计
在纸上勾勒出待构建系统的特征

三大支柱：
- 体系架构：发现 识别 决策一个待构建的系统由多少组成要素构成 决定了软件系统能达到的高度，难易程度，成本核算与任务管理
- 先进的工具：中间件 各种库函数来支撑开发复杂的软件
- 优秀的开发环境：VisualStudio MyEclipse
---

# 组件
组件名称 编号 功能 父类 等
用 CRC 卡表达

每个组件工程意义的设计

**组件的设计**
每个组件需要一个张 CRC 卡：
- 编号
- 名称
- 描述
- 属性值
- 功能
- 所需数据
- 外部接口

SDD
描述的是一张 CRC 卡

组件的发现 设计
## 组件的构成
- **主程序组件**
- 欢迎界面
- 控制组件

- 主程序组件
- GUI boundary 组件
- 业务逻辑组件
- 概念 算法组件
- 数据访问组件

### 主程序组件
程序的入口点。相当于操作系统
`int main(int argc,char** argv) {}`

`class CMyApp: CWinApp {}`
`CFramework`
`CDialogCFormView`
`CDocument`——构建组件的序列化处理

`class MyApp{ public static void main(String args[]) }`

**主程序组件的 CRC 卡**
![](https://github.com/CaesarYangs/MyPictureHotel/blob/main/JuniorClass/SoftwareStructure/%E6%88%AA%E5%B1%8F2022-03-30%2008.31.08.png?raw=true)

CRC 卡在 cpp 中由两个部分来实现：.h 文件与.cpp 文件

### 图形用户界面组件GUI
基于 windows 的应用

*什么是基于图形界面的应用？*
目标是提供易操作易学习易使用的系统，通过**统一化的**、**标准化的**、**各种图形要素组成的**图形用户界面

一种服务系统

- 统一化的图形界面
- 包括以下可视化要素
    - 顶层容器：窗架
    - 各种视窗
    - 菜单条
    - 工具栏
    - 状态栏
- 优点：
    - 提供了易学习易操作 简便的计算机使用处理机制
    - 方便非计算机专业人士进行操作和使用
    - 与具体的硬件设备松耦合
    - 多任务 多线程
    - 标准化，统一化的图形界面

- GUI
    - MFC: GUI 视窗
    - java：AWT Swing
    - ASP.net： 资源编辑器

**需要会识别出常见的图形界面内容和组件**
*窗架如何设计？*
*菜单栏如何设计？*
*各种工具栏如何设计？*
button label 文本框 图文框 

**图形界面主要元素**
![](https://github.com/CaesarYangs/MyPictureHotel/blob/main/JuniorClass/SoftwareStructure/%E6%88%AA%E5%B1%8F2022-04-06%2009.19.25.png?raw=true)

SDI 模型
MDI 模型

- 基于 Dialog 的应用模式
	- CWinAPP
	- CFrameWnd——顶层组件要继承自
- 基于 Java
	- AWT Swing
	- 顶层容器：JFrame
		- JPanel

### 业务逻辑组件
#### Entity



# 开发环境和概念
- AppWIzard
- 组件/类 Wizard
- 资源管理器-将外部资源注入系统
- CDC-绘图区对象：将计算机屏幕当做画布
	- CPen：屏幕上绘图的笔
	- CBrush：屏幕上的刷子
	- BitBlt
---
- MFC：微软设计的，基于开发 window 应用的基本类库
- 工程设计：指生成代码框架
- AppWizard：应用程序生成器/导航器
- ClassWizard：类/组件生成器
- 继承 CWinApp
- 窗架继承 CFrameWnd