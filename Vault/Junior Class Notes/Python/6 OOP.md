# OOP
## [Outline](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=3)

-   面向对象程序设计（Object-Oriented Programming，OOP）尽可能地模拟现实世界。 现实世界是由各种不同事物组成，一切事物皆对象。 面向对象程序设计就是要分析待解决的问题中有哪些对象， 每一类的对象有哪些特点， 不同类的对象之间有什么关系， 互相之间有什么作用。
    
-   面向对象程序设计就是要分析待解决的问题中有 哪些对象

[四大特征](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=4)

## [面向对象编程主要内容](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=6)
1. 类及定义
2. 对象
3. 属性
4. 方法
5. 访问权限
6. 封装 继承 多态


### [1. 类及定义](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=7)
-   类，实例对象，属性，函数和方法。 Python 的类定义由类头（指 class和类名(object)）和统一缩进的类体构成。 object是所有类的父类，可以省略。 类名是一个符合Python标识符命名规则的合法的标识符即可，最好满足“见名知意”的原则，以便增强程序的可读性。

[类的定义](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=8)

-   类相当于模板，一种描述 类对象是通过对类的实例化，类似于函数调用


### [2. 对象](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=9)

-   实例对象是根据类模版生成一个内存体，有确定 的数据与内存地址

[对象的初始化](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=10)

-   面向对象的程序设计中，在对象的实例化时，往往需要对实例（对象）进行初始化，例如设计对象属性的初始值，而这些工作是自动完成的，因此有默认的方法被调用，这个默认的方法就是构造函数 自动被调用，无需显示执行，系统默认执行，如果用户没有重新自定义构造函数方法，系统会执行默认的构造方法
    
-   定义默认参数
    
-   实例化对象c1=Circle(), 传递一个参数c1给[[6 OOP#^f6c080|self]]，得 到默认属性1

    
-   实例化对象c1=Circle(2), 传递2个参数 c1传递给 self 2传递给r，更改了radius的属性
    
-   Self属性

### [3. 属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=12)

-   在类中可以定义一些属性: 类属性，实例属性

[类属性的访问](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=13)

-   类属性虽然归类所有，但实例化的对象都可 以访问类属性
    
-   实例属性通过实例对象可绑定属性，新建、改变 属性

[改变类属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=15)

-   通过类名称改变类属性后，之前或之后实例化的 对象的类属性都会改变
-   更改类属性后，之前或之后实例化的对象的属性都会改变

[通过对象实例改变类属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=16)

-   通过对象实例改变类属性 格式:对象实例.属性=... 如果该对象实例存在这个属性，这个属性的值就被 改变 如果该对象实例不存在这个属性 动为该对象实 例创建一个新的属性

[属性的优先级](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=17)

-   相同名称的实例属性会覆盖掉类属性
    
-   实例属性改变，不影响类属性 相同名称的实例属性优先级高于类属性(覆盖

[不存在该属性时 自动为该对象实例创建一个新的属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=18)

[删除实例属性后，访问该名称对应的属性时，将访问类属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=19)

[不同的实例对象，有不同的实例属性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=20)

[可变对象作为类属性时，需注意每个实例操作都改变其值](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=21)

[使用实例属性替代类属性，以避免实例操作改变 类属性变量的值](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=22)

**[类属性小结](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=23)**

-   不同的实例对象，有不同的实例属性
    
### [4. 方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=24)

-   实例方法 类方法 静态方法

 [self详解](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=25) ^f6c080

-   Self 可看作C++中的this指针进行理解，就是对象自身的意思，在用某个对象调用该方法时，就将该对象作为第一个参数传递给self
    
-   通过实例对象调用的方法

#### [实例方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=27)

-   也可以用类名称Dog调用，但要传递实例参数

#### [类方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=28)

-   在类中可以定义类的方法  通过@classmethod 修饰
    
-   **类方法只能访问类属性，不能访问实例属性**
    
-   第一个参数一般命名为cls (也可以是其他名称

[类方法调用](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=30)

-   一般通过类名称调用

[类方法调用](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=31)

-   也可以通过实例对象调用

#### [静态方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=32)

-   在程序设计中，如果需要在某个类中封装某个方法，该方法既不需要访问实例属性或者调用实例方法，也不需要访问类属性或者调用类方法，可以将该方法封装为静态方法。
    
-   位于类的命名空间中，它不会对任何实例对象进 行操作
    
-   必须通过@staticmethod修饰，不传递参数

[静态方法调用](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=33)

-   与类方法调用不同（传递类参数）
    
-   通过类名称调用，不传递参数，与类方法调用 不同(需要传递类参数
    
-   通过实例对象调用，不传递参数



[类方法及调用小节](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=37)

### [5. 访问权限](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=38)

-   与java和C++ 中类似，存在访问权限问题，即类的属性和方法，存在公有的和私有的之分 在python中更简单
    
-   如果想定义为私有的，在属性前面加两个下划线 __

[私有属性，可以被类内定义的方法访问](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=40)


### [6-2 继承](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=45)

-   面向对象的一个很大特点是类可以被扩展和继承， 继承：创建函数实现功能的复用，若已有一个类，要创建一个与之很像的新类，也可以继承原来的类，避免重复编写代码
    
[子类通过继承可以获得父类的所有方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=46)

-   Pass, 类似于C++ 或Java中的空语句，在python中对应为pass,也可以理解为占位，比如某个函数功能的实现还没有设计好，又不能空着不写，因此可以用pass来替代，占个位置。
    
 [对于父类的方法，子类实现重新定义](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=47)

-   当子类和父类都存在相同的read()方法时，我们说，子类的read()覆盖了父类的read()，在代码运行的时候，总是会调用子类的read()。这样，我们就获得了继承的另一个好处：多态。
    
[设置为私有方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=48)

-   若不想子类覆盖基类的方法，可将方法设为私有

#### ==[重写子类的构造方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=49)==

-   新构造函数没有包含初始化name的代码
    
 [方法1：调用父类的构造函数](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=50)

-   子类必须显示调用父类的构造函数
    

[方法2：使用函数super(推荐使用)](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=51)

-   子类必须显示调用父类的构造函数

#### [为子类中添加新的方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=52)

==[两个重要的内置判定方法](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=53)==

-   在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类，但是反过来不行
    
-   isinstance
    
-   issubclass

[在继承关系中，如果一个实例是某个子类对象 那它也可以被看做是父类实例对象](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=54)

#### [多继承](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=55)
-   一个类可有多个父类，支持多继承

[继承小结](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=57)

-   继承小节 子类把父类的所有功能都直接拿过来，这样就不必 从零做起 子类把父类不适合的方法覆盖(构造函数的重写 若不想子类覆盖父类的方法，将父类方法设为私有 方法 子类可新增自己特有的方法

### [6-3 多态](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=58)
    
-   多态:呈现多种形态
    
-   尽管不知道变量指向的是哪种类型的对象，也能 对其进行操作，且操作的行为会随对象所属的类 型(类)而异

[read twice多态实例](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=59)

-   定义一个两次阅读的函数，传入的参数是一个Person实例

**[只管调用，不管细节](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=61)**

-   无需确切地知道它的子类型，具体是作用在Student 或者Teacher类上呢？无需关心，由运行时该对象的确切类型决定。
    
-   只管调用，不管细节
    
-   只要是Person类或者子类，就会自动调用 实际类型的read( )方法

[Page 63](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=62)

-   Python作为动态语言，则不一定需要传入Person类 型，只需保证传入的对象有一个read( )方法就可以

### [6-1 封装](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=64)

-   将抽象得到的属性和功能相结合，形成一个有机 整体，隐藏对象的属性和实现细节，仅对外提供 公共访问方式的接口 
-   封装:无需知道对象的构造 
-   多态:无需知道对象的类型，就能调用其方法

-   通过 类名. 或者 对象名. 形式访问封装内部的属 性和方法

[封装的好处](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=66)

-   保护隐私、提高安全性
    
-   将变化隔离，便于使用
    
-   提高复用性
    

#### [包](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=68)

-   包(package : 将多个模块分为一个包
    
-   包中包含模块和子包
    
-   包中必须存在__init__.py文件，包的标识，一般不在 __init__.py 中写入模块，尽可能保证简单
    
[包的导入](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=70)

-   Import …. 需要通过完整的名称进行引用

#### [包的导入规则](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=72)

-   from package import item 方式导入包时，这个子项 (item)既可以是子包也可以是其他命名，如函数 类、变量等
    
-   import item.subitem.subsubitem 这样的语法时，这 些子项必须是包，最后的子项可以是包或模块 但不能是类、函数、变量等

---
## [高级特性](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=74)

-   高级特性 生成器 迭代器

### [生成器](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=76)

-   生成器表达式:创建生成器 )替换列表推导 中的[ ]

[生成器实现细节](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=77)

-   generator保存的是算法，每次调用next(g)，就计算出g的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。

[利用生成器的函数](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=80)

-   generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行 我们基本上从来不会用next()来获取下一个返回值，而是直接使用for循环来迭代

*[生成器中拿取返回值](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=81)

-   但是用for循环调用generator时，发现拿不到generator的return语句的返回值。如果想要拿到返回值，必须捕获StopIteration错误，返回值包含在StopIteration的value中：

### [迭代器](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=82)

-   这些可直接作用于for循环的对象统称为可迭代对 象 Iterable

 [迭代器和其它类型的区别](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=83)

> Iter()方法将iterable变为iterator Iterator 是 无限大的数据流，可以看作有序序列，提前并不知道其长度，通过next()不断通过按需计算，返回下一个值。而列表，字典等不能存储无限大的数据流 你可能会问，为什么list、dict、str等数据类型不是Iterator？ 这是因为Python的Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过next()函数实现按需计算下一个数据，所以Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算。 Iterator甚至可以表示一个无限大的数据流，例如全体自然数。而使用list是永远不可能存储全体自然数的。

-   生成器都是Iterator对象，但list、dict str虽然是 Iterable，却不是Iterator

[对可迭代对象，调用iter方法可以返回迭代器对象](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=84)

#### [生成器和迭代器小结](x-devonthink-item://B0002D94-35FA-4CB1-896D-C46D079BCCE2?page=88)

-   生成器和迭代器 生成器:一种特殊的迭代器，保存一种算法，只能 被遍历一次，生成器表达式，生成器函数(yield 创建生成器 迭代器:无限大数据流(容器 ，可通过实现 __iter__( )和__next__( )方法 定义迭代器类，注 意与Iterable可迭代对象区别