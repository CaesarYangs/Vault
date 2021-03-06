## MySQL 索引

### 索引数据结构
*MySQL 数据库使用的索引数据结构是什么?*
**B+树 即 m 路平衡查找树**

B+树是为磁盘或其他直接存取辅助设备设计的一种平衡查找树。在 B+树中,所有记录节点都是按键值的大小顺序存放在同一层的叶子节点上,由各叶子节点指针进行连接。

- **高扇出性**
    - 在数据库中,B+树的高度一般都在 2~4 层,这也就是说查找某一键值的行记录时最多只需要 2 到 4 次 IO,这倒不错。因为当前一般的机械磁盘每秒至少可以做 100 次 IO, 2~4 次的 IO 意味着查询时间只需 0.02~0.04 秒。

数据库中的 B+树索引可以分为**聚集索引(clustered inex)** 和**辅助索引(secondary index)**。

*假设每条 sql 信息为 1kb,主键 ID 为 bigint 型,一颗高度为 4 的 b+树能存储多少数据？*
*如果是 2 层的 B + 树,最多可以存储多少行数据?*
在 innodb 存储引擎里面,最小的存储单元是页(page), 一个页的大小是 16KB。

假设一行数据的大小是 1k,那么一个页可以存放 16 行这样的数据。那如果想查找某个页里面的一个数据的话,得首先找到他所在的页。innodb 存储引擎我们都知道使用 B + 树的结构来组织数据。如果是在主键上建立的索引就是聚簇索引,即只有在叶子节点才存储行数据,而非叶子节点里面的内容其实是键值和指向数据页的指针。

*为什么选用 B+树做索引而不选用二叉树或者 B 树？*
- 与普通二叉查找树的不同
    - 要考虑磁盘 IO 的影响,它相对于内存来说是很慢的。数据库索引是存储在磁盘上的,当数据量大时, 就不能把整个索引全部加载到内存了,只能逐一加载每一个磁盘页(对应索引树的节点)。
    - 所以要减少 IO 次数,对于树来说,IO 次数就是树的高度,而 “矮胖” 就是 b 树的特征之一,它的每个节点最多包含 m 个孩子, m 称为 b 树的阶。
- 为普通 B-树有的不同
    - B+树就是 B 树（B-树）的一种变体
    - **查询效率更高**
        - b + 树的中间节点不保存数据,所以磁盘页能容纳更多节点元素,更 “矮胖”。B 树不管叶子节点还是非叶子节点,都会保存数据,这样导致在非叶子节点中能保存的指针数量变少(有些资料也称为扇出),指针少的情况下要保存大量数据,只能增加树的高度,导致 IO 操作变多,查询性能变低;
    - **查询效率更稳定**
        - b + 树查询必须查找到叶子节点,b 树只要匹配到即可直接返回。因此 b + 树查找更稳定(并不慢),必须查找到叶子节点;而 B 树,如果数据在根节点,最快,在叶子节点最慢,查询效率不稳定。
    - **查找路径优化（范围查找）——双路径查找**
        - 对于范围查找来说,b + 树只需遍历叶子节点链表即可,并且不需要排序操作,因为叶子节点已经对索引进行了排序操作。b 树却需要重复地中序遍历,找到所有的范围内的节点。

*为什么用 B+ 树做索引而不用哈希表做索引?*
- **哈希表方法模糊查找不支持**
    - 哈希表是把索引字段映射成对应的哈希码然后再存放在对应的位置, 这样的话,如果我们要进行模糊查找的话,显然哈希表这种结构是不支持的,只能遍历这个表。而 B + 树则可以通过最左前缀原则快速找到对应的数据。
- **哈希表范围查找不支持**
    - 如果我们要进行范围查找,例如查找 ID 为 100 ~ 400 的人,哈希表同样不支持,只能遍历全表。
- **哈希冲突问题严重**
    - 索引字段通过哈希映射成哈希码,如果很多字段都刚好映射到相同值的哈希码的话,那么形成的索引结构将会是一条很长的链表,这样的话,查找的时间就会大大增加。

### 最左前缀
*什么是最左前缀原则？*
- **最左前缀原则**
    - 由于在 B + 树结构的索引中,索引项是按照索引定义里面出现的字段顺序排序的,索引在查找的时候, 可以快速定位到 ID 为 100 的张一,然后直接向右遍历所有张开头的人,直到条件不满足为止。
    - 也就是说,找到第一个满足条件的人之后,直接向右遍历就可以了,由于索引是有序的,所有满足条件的人都会聚集在一起。
    - <u>而这种定位到最左边,然后向右遍历寻找,就是我们所说的最左前缀原则。</u>

### 聚集索引
聚集索引(clustered index)就是按照每张表的主键构造一棵 B+树,同时叶子节点中存放的即为整张表的行记录数据,也将聚集索引的叶子节点称为数据页。每个数据页都通过一个双向链表来进行链接。

由于实际的数据页只能按照一棵 B+树进行排序,因此每张表只能拥有一个聚集索引。在多数情况下,查询优化器倾向于采用聚集索引。因为聚集索引能够在 B+树索引的叶子节点上直接找到数据。此外,由于定义了数据的逻辑顺序,它对于主键的排序查找和范围查找速度非常快。叶子节点的数据就是用户所要查询的数据

> `SELECT * FROM Profile ORDER BY id LIMIT 10;`
>
> 虽然使用 ORDER BY 对主键 id 记录进行排序,但是在实际过程中并没有进行所谓的 filesort 操作,而这就是因为聚集索引的特点。另一个是范围查询(range query),即如果要查找主键某一范围内的数据,通过叶子节点的上层中间节点就可以得到页的范围,之后直接读取数据页即可。如: SELECT * FROM Profile where id > 1 and id <100;

### 辅助索引
对于辅助索引(Secondary Index,也称非聚集索引),叶子节点并不包含行记录的全部数据。叶子节点除了包含键值以外,每个叶子节点中的索引行中还包含了一个书签(bookmark)。该书签用来告诉 InnoDB 存储引擎哪里可以找到与索引相对应的行数据。由于 InnoDB 存储引擎表是索引组织表,因此 InnoDB 存储引擎的辅助索引的书签就是相应行数据的聚集索引键。

辅助索引的存在并不影响数据在聚集索引中的组织,因此每张表上可以有多个辅助索引。当通过辅助索引来寻找数据时,InnoDB 存储引擎会遍历辅助索引并通过叶级别的指针获得指向主键索引的主键,然后再通过主键索引来找到一个完整的行记录。举例来说,如果在一棵高度为 3 的辅助索引树中查找数据,那需要对这棵辅助索引树遍历 3 次找到指定主键,如果聚集索引树的高度同样为 3,那么还需要对聚集索引树进行 3 次查找,最终找到一个完整的行数据所在的页,因此一共需要 6 次逻辑 IO 访问以得到最终的一个数据页。

*如何选择表的列索引从而使得更加高效？*
> `SELECT*FROM student WHERE sex='M'`
> 按性别进行查询时,可取值的范围一般只有'M'、'F'。因此上述 SQL 语句得到的结果可能是该表 50% 的数据(假设男女比例 1∶1),这时添加 B+树索引是完全没有必要的。相反,如果某个字段的取值范围很广,几乎没有重复,即属于高选择性,则此时使用 B+树索引是最适合的。
>
> 怎样查看索引是否是高选择性的呢?可以通过 SHOW INDEX 结果中的列 Cardinality 来观察。Cardinality 值非常关键,表示索引中不重复记录数量的预估值。同时需要注意的是,Cardinality 是一个预估值,而不是一个准确值,基本上用户也不可能得到一个准确的值。在实际应用中,Cardinality/n_rows_in_table 应尽可能地接近 1。如果非常小,那么用户需要考虑是否还有必要创建这个索引。

### 实操
#### 联合索引
联合索引是指对表上的多个列进行索引。

- 情况 1: 如果只对于 userid 进行查询,如: `SELECT*FROM buy_log WHERE userid=2`; 索引选择:优化器最终的选择是索引 userid,因为该索引的叶子节点包含单个键值,所以理论上一个页能存放的记录应该更多。
- 情况 2: `SELECT*FROM buy_log WHERE userid=1 ORDER BY buy_date DESC LIMIT 3;` 索引选择:优化器使用了(userid,buy_date)的联合索引 userid_2,因为在这个联合索引中 buy_date 已经排序好了。根据该联合索引取出数据,无须再对 buy_date 做一次额外的排序操作。
- 情况 3:假如三个字段的联合索引。如:对于联合索引(a,b,c)来说,下列语句同样可以直接通过联合索引得到结果,不需要 filesort 的排序操作:
    - `SELECT...FROM TABLE WHERE a=xxx ORDER BY b`
    - `SELECT...FROM TABLE WHERE a=xxx AND b=xxx ORDER BY c`
    - 但是对于下面的语句,联合索引不能直接得到结果,其还需要执行一次 filesort 排序操作,因为索引(a,c)并未排序: `SELECT...FROM TABLE WHERE a=xxx ORDER BY c`

#### 覆盖索引

### 索引底层
*MySQL 是如何获取索引所在内存中的数据页的*
哈希表,利用哈希算法。
哈希算法是一种常见算法,时间复杂度为 O(1),且不只存在于索引中,每个数据库应用中都存在该数据库结构。

数据库中一般采用除法散列的方法,发生碰撞时采用链地址法。
在哈希函数的除法散列法中,通过取 k 除以 m 的余数,将关键字 k 映射到 m 个槽的某一个去,即哈希函数为: h(k)=k mod m

InnoDB 存储引擎使用哈希算法来对字典进行查找,其冲突机制采用链表方式,哈希函数采用除法散列方式。对于缓冲池页的哈希表来说,在缓冲池中的 Page 页都有一个 chain 指针,它指向相同哈希函数值的页。
而对于除法散列,m 的取值为略大于 2 倍的缓冲池页数量的质数。

> 例如:当前参数 innodb_buffer_pool_size 的大小为 10M,则共有 640 个 16KB 的页。对于缓冲池页内存的哈希表来说,需要分配 640×2=1280 个槽, 但是由于 1280 不是质数,需要取比 1280 略大的一个质数,应该是 1399,所以在启动时会分配 1399 个槽的哈希表,用来哈希查询所在缓冲池中的页。

### 全文检索
`SELECT*FROM blog WHERE content like'%xxx%'`

根据 B+树索引的特性,上述 SQL 语句即便添加了 B+树索引也是需要进行索引的扫描来得到结果。类似这样的需求在互联网应用中还有很多。例如,搜索引擎需要根据用户输入的关键字进行全文查找,电子商务网站需要根据用户的查询条件,在可能需要在商品的详细介绍中进行查找,这些都不是 B+树索引所能很好地完成的工作。

全文检索(Full-Text Search)是将存储于数据库中的整本书或整篇文章中的任意内容信息查找出来的技术。它可以根据需要获得全文中有关章、节、段、句、词等信息,也可以进行各种统计和分析。

在之前的 MySQL 数据库中,InnoDB 存储引擎并不支持全文检索技术。大多数的用户转向 MyISAM 存储引擎, 这可能需要进行表的拆分,并将需要进行全文检索的数据存储为 MyISAM 表。这样的确能够解决逻辑业务的需求,但是却丧失了 InnoDB 存储引擎的事务性,而这在生产环境应用中同样是非常关键的。

InnoDB 存储引擎从 1.2.x 版本开始支持全文检索的技术,其采用 full inverted index 的方式。在 InnoDB 存储引擎中,将(DocumentId,Position)视为一个“ilist”。因此在全文检索的表中,有两个列,一个是 word 字段,另一个是 ilist 字段,并且在 word 字段上有设有索引。

## InnoDB 引擎
InnoDB 存储引擎表是索引组织表,即表中数据按照主键顺序存放。

### InnoDB 锁
- 共享锁（S Lock）：允许事务读一行数据。
- 排他锁（X Lock）：允许事务删除或更新一行数据。

如果一个事务 T1 已经获得了行 r 的共享锁,那么另外的事务 T2 可以立即获得行 r 的共享锁,因为读取并没有改变行 r 的数据,称这种情况为锁兼容(Lock Compatible)。但若有其他的事务 T3 想获得行 r 的排他锁,则其必须等待事务 T1、T2 释放行 r 上的共享锁——这种情况称为锁不兼容。

**排他锁 共享锁的兼容性**

|     | X      | S      |
| --- | ------ | ------ |
| X   | 不兼容 | 不兼容 |
| S   | 不兼容 | 兼容   |

### InnoDB 主键自增长
自增长在数据库中是非常常见的一种属性,也是很多 DBA 或开发人员首选的主键方式。在 InnoDB 存储引擎的内存结构中,对每个含有自增长值的表都有一个自增长计数器(auto-increment counter)。当对含有自增长的计数器的表进行插入操作时,这个计数器会被初始化,执行如下的语句来得到计数器的值:
`SELECT MAX(auto_inc_col)FROM t FOR UPDATE;`

插入操作会依据这个自增长的计数器值加 1 赋予自增长列。这个实现方式称做 AUTO-INC Locking。**这种锁其实是采用一种特殊的表锁机制,为了提高插入的性能,锁不是在一个事务完成后才释放,而是在完成对自增长值插入的 SQL 语句后立即释放。**

虽然 AUTO-INC Locking 从一定程度上提高了并发插入的效率,但还是存在一些性能上的问题。首先,对于有自增长值的列的并发插入性能较差,事务必须等待前一个插入的完成(虽然不用等待事务的完成)。其次,对于 INSERT…SELECT 的大数据量的插入会影响插入的性能,因为另一个事务中的插入会被阻塞。

### InnoDB 行锁
InnoDB 存储引擎有 3 种行锁的算法,其分别是:
- Record Lock:单个行记录上的锁
- Gap Lock:间隙锁,锁定一个范围,但不包含记录本身
- Next-Key Lock∶Gap Lock+Record Lock,锁定一个范围,并且锁定记录本身

Record Lock 总是会去锁住索引记录,如果 InnoDB 存储引擎表在建立的时候没有设置任何一个索引,那么这时 InnoDB 存储引擎会使用隐式的主键来进行锁定。
Next-Key Lock 是结合了 Gap Lock 和 Record Lock 的一种锁定算法,在 Next-Key Lock 算法下,InnoDB 对于行的查询都是采用这种锁定算法。

### 与 mylsam 的区别
1. 是否支持行级锁 : MyISAM 只有表级锁 (table-level locking),而 InnoDB 支持行级锁 (rowlevel locking) 和表级锁 , 默认为行级锁。
2. 是否支持事务和崩溃后的安全恢复: MyISAM 强调的是性能,每次查询具有原子性 , 其执行速度比 InnoDB 类型更快,但是不提供事务支持。但是 InnoDB 提供事务支持事务,外部键等高级数据库功能。具有事务 (commit)、回滚 (rollback) 和崩溃修复能力 (crash recovery capabilities) 的事务安全 (transaction-safe (ACID compliant)) 型表。
3. 是否支持外键: MyISAM 不支持,而 InnoDB 支持。
4. 是否支持 MVCC:仅 InnoDB 支持。应对高并发事务 , MVCC 比单纯的加锁更高效 ;MVCC 只在 READ COMMITTED 和 REPEATABLE READ 两个隔离级别下工作 ;MVCC 可以使用乐观 (optimistic) 锁和悲观 (pessimistic) 锁来实现 ; 各数据库中 MVCC 实现并不统一。‘

## MySQL 语句执行原理


## 优化
### MySQL 单表优化


### 表拆分


## 其他
### 脏读
脏读指的就是在不同的事务下,当前事务可以读到另外事务未提交的数据,简单来说就是可以读到脏数据。

1. 脏读 ：脏读就是指当一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问 这个数据，然后使用了这个数据。  
脏读现象在生产环境中并不常发生,从上面的例子中就可以发现,脏读发生的条件是需要事务的隔离级别为 READ UNCOMMITTED,而目前绝大部分的数据库都至少设置成 READ COMMITTED。

### 幻读
- 幻读 : 是指当事务不是独立执行时发生的一种现象，例如第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行。 同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。那么，以后就会发生操作第一个事务的用户发现表中还有没有修改的数据行，就好象 发生了幻觉一样。例如，一个编辑人员更改作者提交的文档，但当生产部门将其更改内容合并到该文档的主复本时，发现作者已将未编辑的新材料添加到该文档中。 如果在编辑人员和生产部门完成对原始文档的处理之前，任何人都不能将新材料添加到文档中，则可以避免该问题。

### 不可重复度
- 不可重复读 ：是指在一个事务内，多次读同一数据。在这个事务还没有结束时，另外一个事务也访问该同一数据。那么，在第一个事务中的两 次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样就发生了在一个事务内两次读到的数据是不一样的，因此称为是不 可重复读。例如，一个编辑人员两次读取同一文档，但在两次读取之间，作者重写了该文档。当编辑人员第二次读取文档时，文档已更改。原始读取不可重复。如果 只有在作者全部完成编写后编辑人员才可以读取文档，则可以避免该问题。  


### 丢失更新
丢失更新是另一个锁导致的问题,简单来说其就是一个事务的更新操作会被另一个事务的更新操作所覆盖,从而导致数据的不一致。
例如:
1)事务 T1 将行记录 r 更新为 v1,但是事务 T1 并未提交。
2)与此同时,事务 T2 将行记录 r 更新为 v2,事务 T2 未提交。
3)事务 T1 提交。
4)事务 T2 提交。
但是,在当前数据库的任何隔离级别下,都不会导致数据库理论意义上的丢失更新问题。这是因为,即使是 READ UNCOMMITTED 的事务隔离级别,对于行的 DML 操作,需要对行或其他粗粒度级别的对象加锁。因此在上述步骤 2)中, 事务 T2 并不能对行记录 r 进行更新操作,其会被阻塞,直到事务 T1 提交。

虽然数据库能阻止丢失更新问题的产生,但是在生产应用中还有另一个逻辑意义的丢失更新问题,而导致该问题的并不是因为数据库本身的问题。

### 数据库死锁
死锁是指两个或两个以上的事务在执行过程中,因争夺锁资源而造成的一种互相等待的现象。若无外力作用,事务都将无法推进下去。解决死锁问题最简单的方式是不要有等待,将任何的等待都转化为回滚,并且事务重新开始。毫无疑问,这的确可以避免死锁问题的产生。然而在线上环境中,这可能导致并发性能的下降,甚至任何一个事务都不能进行。而这所带来的问题远比死锁问题更为严重,因为这很难被发现并且浪费资源。

解决死锁问题最简单的一种方法是超时,即当两个事务互相等待时,当一个等待时间超过设置的某一阈值时,其中一个事务进行回滚,另一个等待的事务就能继续进行。在 InnoDB 存储引擎中,参数 innodb_lock_wait_timeout 用来设置超时的时间。

超时机制虽然简单,但是其仅通过超时后对事务进行回滚的方式来处理,或者说其是根据 FIFO 的顺序选择回滚对象。但若超时的事务所占权重比较大,如事务操作更新了很多行,占用了较多的 undo log,这时采用 FIFO 的方式, 就显得不合适了,因为回滚这个事务的时间相对另一个事务所占用的时间可能会很多。

因此,除了超时机制,当前数据库还都普遍采用 wait-for graph(等待图)的方式来进行死锁检测。较之超时的解决方案,这是一种更为主动的死锁检测方式。InnoDB 存储引擎也采用的这种方式。wait-for graph 要求数据库保存以下两种信息: 锁的信息链表事务等待链表


## **事务隔离级别**
SQL 标准定义了四种隔离级别，MySQL 全都支持。这四种隔离级别分别是：

1.  读未提交（READ UNCOMMITTED）
2.  读提交 （READ COMMITTED）
3.  可重复读 （REPEATABLE READ）
4.  串行化 （SERIALIZABLE）

从上往下，隔离强度逐渐增强，性能逐渐变差。采用哪种隔离级别要根据系统需求权衡决定，其中，**可重复读**是 MySQL 的默认级别。