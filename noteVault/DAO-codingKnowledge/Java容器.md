# Overview
**Collection**
- List
    ArrayList
    LinkedList
    Vector
    Stack
- Set
    HashSet
    LinkedHashSet
    TreeSet
- Map
    HashMap/Linked HashMap
    TreeMap
    ConcurrentHashMap
    HashTable

# Collection
## List


## Set
Set不允许包含相同的元素,如果试图把两个相同元素加入同一个集合中,add方法返回false。
Set判断两个对象相同不是使用运算符,而是根据equals方法。
也就是说,只要两个对象用equals方法比较返回true,Set就不会接受这两个对象。


### HashSet
HashSet 的实现依赖于 HashMap

### LinkedHashSet

### TreeSet
与 HashSet 和 LinkedHashSet 一个套路,TreeSet 其实是使用了 TreeMap 的结构。


# Map

## HashMap
本质是一个定长数组，数组内存放的是链表。是一个 Entry 类型的数组。
**即：是一个[[邻接表]]表示的哈希数据结构**

就是一个数组+单向链表结构

**Entry 数组源码：**
```java
static class Entry<K,V> implements Map.Entry<K,V> {
        final K key;
        V value;
        Entry<K,V> next;//存储指向下一个Entry的引用，单链表结构
        final int hash;//对key的hashcode值进行hash运算后得到的值，存储在Entry，避免重复计算

        /**
         * Creates new entry.
         */
        Entry(int h, K k, V v, Entry<K,V> n) {
            value = v;
            next = n;
            key = k;
            hash = h;
        }
```

> 存放了 k，v 的值以及指向下一个元素的引用

**操作过程：**
通过 hash 计算出放在数组中的位置（若该位置已经有元素了，则插入到链表头 JDK1.7/链表尾 JDK1.8）。
*最先插入的元素在链表尾部。邻接表的每第一个元素存放的是最后插入的元素*

### Put 方法
- JDK7 采用位桶+链表方式——即散列链表方式
- JDK8 采用位桶+链表/红黑树方式

```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }

```

真正的 hash 值存储在 table 位置的 index 中

***计算数据下标***
1.  计算哈希码：`h=key.HashCode()` 根据 key 值，利用 hashcode()计算
2.  二次处理哈希码-最终求得 key 对应的哈希值：`h^(h>>>16)` 即扰动处理 #还不太会
    本质：二次处理低位 = 哈希码的高 16 位不变，低 16 位 = 低 16 位 XOR 高 16 位
3.  最终计算存储的数组位置：`h & (length-1)` 即二次处理后的哈希码 与运算(&)（数组长度-1）

### hash 值计算
```java
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

- 当 key=null 时，hash 值为 0，因此所以 hash 值才可以是 null
注：HashTable 的 key 不可以为 null 为 null 的 key 不能使用 `hashCode()`
- 当 key 不是 null 时，通过先计算 key 的 hashcode（记为 h）。然后对哈希吗进行扰动处理：按位 异或(^) 哈希码自身右移 16 位后的二进制

整个计算的步骤：
1.  计算哈希码
2.  二次处理哈希码
3.  最终计算存储的数组位置

| 步骤                     | 代码实现           | 具体计算过程                                                                      |
| ------------------------ | ------------------ | --------------------------------------------------------------------------------- |
| 1.计算哈希码             | h = key.hashCode() | 根据键 key，通过 hashCode()计算                                                     |
| 2.二次处理哈希码         | h^(h>>>16)         | 扰动处理 本质：哈希码高 16 位不变 低 16 位=低 16 位 异或 高 16 位（即：高位参与低位运算） |
| 3.最终计算存储的数组位置 | h&(length-1)       | 即 二次处理后的哈希码 与运算(&)(数组长度-1)                                                                                  |

*HashMap 中插入一条数据，如何计算数组下标*

*为什么 hash 要进行右移 16 位 XOR 运算*
> 由于和最终和(length-1)运算,length 绝大多数情况小于 2 的 16 次方。所以始终是 hashcode 的低 16 位(甚至更低)参与运算。要是高 16 位也参与运算,会让得到的下标更加散列。所以这样高 16 位是用不到的,如何让高 16 也参与运算呢。所以才有 hash(Object key)方法。让他的 hashCode()和自己的高 16 位^运算。所以(h >>> 16)得到他的高 16 位与 hashCode()进行^运算。

### 转换为红黑树
**红黑树的引入**
JDK1.7 之前 HashMap 的数据结构为 数组+链表

链表来存储 hash 值一样的 key-value. 如果按照链表的方式存储,随着节点的增加数据会越来越多,这会导致查询节点的时间复杂度会逐渐增加,平均时间复杂度 O(n)。
<u>为了提高查询效率,故在 JDK1.8 中引入了改进方法红黑树。此数据结构的平均查询效率为 O(log n) 。</u>

**转换为红黑树——链表长度为 8 时进行相应转换**
树节点所占空间是普通节点的两倍,所以只有当节点足够多的时候,才会使用树节点。

> 节点少的时候,尽管时间复杂度上,红黑树比链表好一点,但是红黑树所占空间比较大,综合考虑,认为只能在节点太多的时候,红黑树占空间大这一劣势不太明显的时候,才会舍弃链表,使用红黑树,这也是为什么不直接全部使用红黑树的原因。

以空间换时间--以时间换空间

在理想状态下,受随机分布的 hashCode 影响,链表中的节点遵循泊松分布,而且根据统计,链表中节点数是 8 的概率已经接近千分之一,而且此时链表的性能已经很差了。所以在这种比较罕见和极端的情况下,才会把链表转变为红黑树。因为链表转换为红黑树也是需要消耗性能的,特殊情况特殊处理,为了挽回性能,权衡之下,才使用红黑树,提高性能。

**链表长度大于 8 时也不一定转换为红黑树**
可以看到在 treeifyBin 中并不是简单地将链表转换为红黑树,而是先判断 table 的长度是否大于 64,如果小于 64,就通过扩容的方式来解决,避免红黑树结构化。

**AVL 树与红黑树的使用选择** [[5 树]]
AVL 树和红黑树有几点比较和区别:
1.  AVL 树是更加严格的平衡,因此可以提供更快的查找速度,一般读取查找密集型任务,适用 AVL 树。
2.  红黑树更适合于插入修改密集型任务。
3.  通常,AVL 树的旋转比红黑树的旋转更加难以平衡和调试。

*HashMap 为什么不直接使用 hashCode() 处理后的哈希值直接作为数组下标？*
hashCode()方法返回的是 int 整数类型,其范围为-(2 ^ 31)~(2 ^ 31-1),约有 40 亿个映射空间,而 HashMap 的容量范围是在 16(初始化默认值)~2 ^ 30,HashMap 通常情况下是取不到最大值的,并且设备上也难以提供这么多的存储空间,从而导致通过 hashCode()计算出的哈希值可能不在数组大小范围内,进而无法匹配存储位置。

**hashmap 的数组长度要保持为 2 的幂次方**
若不按此要求进行，空间浪费相当大,更糟的是这种情况中,数组可以使用的位置比数组长度小了很多,这意味着进一步增加了碰撞的几率,减慢了查询的效率!这样就会造成空间的浪费。

**JDK1.7 与 JDK1.8 的 HashMap 实现区别**

### 扩容
**JDK1.7**
1.7 中整个扩容过程就是一个取出数组元素(实际数组索引位置上的每个元素是每个独立单向链表的头部,也就是发生 Hash 冲突后最后放入的冲突元素)然后遍历以该元素为头的单向链表元素,依据每个被遍历元素的 hash 值计算其在新数组中的下标然后进行交换(即原来 hash 冲突的单向链表尾部变成了扩容后单向链表的头部)。

**JDK1.8**
在 JDK 1.8 中 HashMap 的扩容操作就显得更加的骚气了, 由于扩容数组的长度是 2 倍关系,所以对于假设初始 tableSize = 4 要扩容到 8 来说就是 0100 到 1000 的变化(左移一位就是 2 倍),在扩容中只用判断原来的 hash 值与左移动的一位(newtable 的值)按位与操作是 0 或 1 就行,0 的话索引就不变,1 的话索引变成原索引加上扩容前数组。

**String 类适合做 HashMap Key 的原因**
> 设计 hashCode() 时最重要的因素就是对同一个对象调用 hashCode() 都应该产生相同的值。
> ——Java 编程思想

String 类型的对象对这个条件有着很好的支持,因为 String 对象的 hashCode() 值是根据 String 对象的内容计算的,并不是根据对象的地址计算。下面是 String 类源码中的 hashCode() 方法: String 对象底层是一个 final 修饰的 char 类型的数组,hashCode() 的计算是根据字符数组的每个元素进行计算的,所以内容相同的 String 对象会产生相同的散列码。

### 自定义 Key
**重写 HashCode( )**

**重写 equals( )**

### 哈希冲突
Hash,一般翻译为“散列”,也有直接音译为“哈希”的,这就是把任意长度的输入通过散列算法,变换成固定长度的输出,该输出就是散列值(哈希值);这种转换是一种压缩映射, 也就是,散列值的空间通常远小于输入的空间,不同的输入可能会散列成相同的输出,所以不可能从散列值来唯一的确定输入值。简单的说就是一种将任意长度的消息压缩到某一固定长度的消息摘要的函数。

所有散列函数都有如下一个基本特性:根据同一散列函数计算出的散列值如果不同,那么输入值肯定也不同。但是,根据同一散列函数计算出的散列值如果相同(哈希冲突情况), 输入值不一定相同。

### 负载因子
*负载因子为什么 如何影响 HashMap 性能？*
负载因子表示一个散列表的空间的使用程度

所以负载因子越大则散列表的装填程度越高,也就是能容纳更多的元素,元素多了,链表大了,所以此时索引效率就会降低。
反之,负载因子越小则链表中的数据量就越稀疏,此时会对空间造成烂费,但是此时索引效率高。

## HashTable
HashTable 同样也是线程安全的。

**HashTable 与 HashMap 的不同**：

**1. 继承的父类不同**
Hashtable 继承自 Dictionary 类,而 HashMap 继承自 AbstractMap 类。但二者都实现了 Map 接口

**2. 线程安全性不同**
javadoc 中关于 hashmap 的一段描述如下:此实现不是同步的。如果多个线程同时访问一个哈希映射, 而其中至少一个线程从结构上修改了该映射,则它必须保持外部同步。

Hashtable 中的方法是 Synchronize 的,而 HashMap 中的方法在缺省情况下是非 Synchronize 的。

**3. 是否提供 `contains` 方法**
HashMap 把 Hashtable 的 contains 方法去掉了,改成 containsValue 和 containsKey,因为 contains 方法容易让人引起误解。
Hashtable 则保留了 contains,containsValue 和 containsKey 三个方法,其中 contains 和 containsValue 功能相同。

**4. key 和 value 是否允许 null 值**
其中 key 和 value 都是对象,并且不能包含重复 key,但可以包含重复的 value。

**Hashtable 中,key 和 value 都不允许出现 null 值。** 但是如果在 Hashtable 中有类似 put(null,null)的操作, 编译同样可以通过,因为 key 和 value 都是 Object 类型,但运行时会抛出 NullPointerException 异常,这是 JDK 的规范规定的。

**HashMap 中,null 可以作为键,这样的键只有一个;可以有一个或多个键所对应的值为 null。** 当 get()方法返回 null 值时,可能是 HashMap 中没有该键,也可能使该键所对应的值为 null。因此,在 HashMap 中不能由 get()方法来判断 HashMap 中是否存在某个键, 而应该用 containsKey()方法来判断。

**5. 两数据结构的内部遍历方式实现不同**
Hashtable、HashMap 都使用了 Iterator。而由于历史原因,Hashtable 还使用了 Enumeration 的方式 。

**6. hash 值不同**
哈希值的使用不同,HashTable 直接使用对象的 hashCode。而 HashMap 重新计算 hash 值。

**7. 内部使用的数组初始化和扩容方式不同**
HashTable 在不指定容量的情况下的默认容量为 11,而 HashMap 为 16,Hashtable 不要求底层数组的容量一定要为 2 的整数次幂,而 HashMap 则要求一定为 2 的整数次幂。

Hashtable 扩容时,将容量变为原来的 2 倍加 1,而 HashMap 扩容时,将容量变为原来的 2 倍。      Hashtable 和 HashMap 它们两个内部实现方式的数组的初始大小和扩容的方式。HashTable 中 hash 数组默认大小是 11,增加的方式是 old*2+1。

## LinkedHashMap
LinkedHashMap 是继承于 HashMap,是基于 HashMap 和双向链表来实现的。

HashMap 无序;LinkedHashMap 有序,可分为插入顺序和访问顺序两种。如果是访问顺序,那 put 和 get 操作已存在的 Entry 时,都会把 Entry 移动到双向链表的表尾(其实是先删除再插入)。

LinkedHashMap 存取数据,还是跟 HashMap 一样使用的 Entry[]的方式,双向链表只是为了保证顺序。

LinkedHashMap 是线程不安全的。

### 维护双向链表

总得来说,LinkedHashMap 底层是数组+单向链表+双向链表。
数组加单向链表就是 HashMap 的结构,记录数据用;双向链表,存储插入顺序用。

在 LinkedHashMap 中,是通过双联表的结构来维护节点的顺序的。实际上在内存中的情况如下图所示,每个节点都进行了双向的连接,维持插入的顺序(默认)。
head 指向第一个插入的节点,tail 指向最后一个节点。

![](https://1.bp.blogspot.com/-fW_E_QPoc0E/XeDe5AhRZVI/AAAAAAAAGkE/Kh2Pl0U6ibkSezgh9e7i3fM2raciXE-bwCLcBGAsYHQ/s1600/How%2BLinkedHashMap%2Bworks.png)
### 两种访问顺序

### LinkedHashMap 应用
**1. 用 LinkedHashMap 实现一个简易的缓存清理(LRU 算法)**
[[5 存储管理#^ed8554|操作系统 内存页面置换算法：LRU 最近最久未使用]]

## ConcurrentHashMap
**即：支持并发的 HashMap**
与 HashTable 类似，但多线程下效率更高。

引入并发，引入锁

## TreeMap
