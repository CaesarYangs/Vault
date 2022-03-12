
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

# HashMap
本质是一个定长数组，数组内存放的是链表。是一个Entry类型的数组。
**即：是一个[[邻接表]]表示的哈希数据结构**

**Entry数组源码：**
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

> 存放了k，v的值以及指向下一个元素的引用

**操作过程：**
通过hash计算出放在数组中的位置（若该位置已经有元素了，则插入到链表头JDK1.7/链表尾JDK1.8）。
*最先插入的元素在链表尾部。邻接表的每第一个元素存放的是最后插入的元素*

## Put方法
- JDK7采用桶+链表方式——即散列链表方式
- JDK8采用位桶+链表/红黑树方式


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

真正的hash值存储在table位置的index中

***计算数据下标***
1. 计算哈希码：`h=key.HashCode()` 根据key值，利用hashcode()计算
2. 二次处理哈希码-最终求得key对应的哈希值：`h^(h>>>16)` 即扰动处理 #还不太会
	本质：二次处理低位 = 哈希码的高16位不变，低16位 = 低16位 XOR 高16位
3. 最终计算存储的数组位置：`h & (length-1)` 即二次处理后的哈希码 与运算(&)（数组长度-1）




## hash值计算
```java
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

- 当key=null时，hash值为0，因此所以hash值才可以是null
- 当key不是null时，通过先计算key的hashcode（记为h）
	然后对哈希吗进行扰动处理：按位 异或(^) 哈希码自身右移16位后的二进制

***为什么hash要进行右移16位 XOR运算***


## Hashmap
