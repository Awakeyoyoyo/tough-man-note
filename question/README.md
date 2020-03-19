# 面试问题

# 简介

顺手记录看到的面试问题以及答案

## hashMap

**1.HashMap的数据结构？**

hashmap采取数组+链表的数据结构，在遇到哈希冲突的时候采用链表结构来解决哈希冲突，jdk1.8后分成了两种情况，bucket中元素个数大于8的时候，自动转换为红黑树的结构。目的是因为链表的查询速度比较慢，元素越多越明显，改成红黑树是为了提高查询速度。

#### 2.hashmap为什么线程不安全？



####  3.hashmap为什么数组长度一定是2的次方？

#### 

#### 4.HashMap是否线程安全？

不安全  hashtable安全

#### **5.如果想使用线程安全的HashMap该如何做？**

 Collections的synchronizedMap() 方法使HashMap具有同步的能力

Map map = Collections.synchronizedMap(new HashMap());

或者使用ConcurrentHashMap

使用hashtable也可以

HashTable主要支持同步和但不允许null作为key和value，任一时刻只有一个线程能写Hashtable，即线程安全），因此也导致了 Hashtable 在写入时会比较慢。

#### 6.jdk1.7与1.8中的hashmap的扩容方法有何不同，并且做了什么改良

jdk1.8haspmap的resize函数分析

```java
    final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                          //通过(e.hash & oldCap) == 0来判断是否需要移位，如果为真则在原位不动, 
                            if ((e.hash & oldCap) == 0) {
                              //尾插法
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                              //尾插法
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                         // 当前hash槽位 + oldCap的位置;
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }

```

不同之处在于：

##### 1）1.8不再为元素一一重新计算下标，而是分成两类，一类不需要计算直接用原来的下标，一类为原下标+原tables数组的长度

##### 2）

### 最精髓之处：为何 e.hash & oldCap == 0为什么可以判断当前节点是否需要移位, 而不是再次计算hash;

记得这个计算桶下表运算吗

```java
static int indexFor(int h, int length) { 
  //jdk1.7的源码，jdk1.8没有这个方法，但是实现原理一样的,在方法体中运用
     return h & (length-1);  //第三步 与运算
}
```

```java
   //默认大小16的时候
	 old:
   26: 0001 1010
   15: 0000 1111
    &: 0000 1010    
    //扩容一倍之后
   new:
   26: 0001 1010
   31: 0001 1111
    &: 0001 1010
```

两个函数结合看就知道为什么了。其实因为扩容一倍之后呢，h&(length-1）等于左边多了一位，所以如果oldcap获取的值根据原来来看是tables的长度即16，恰好就是多左边多出来的那位。0001 0000,所以 e.hash & oldCap == 0如果不是等于0 代表示它高位的第四位是为1，即它通过indexfox计算的下标会与原来的不同（即没有了冲突），所以可以鉴定出出它是需要移位的。

```
newTab[j + oldCap] = hiHead;
```

那为什么j + oldCap就是他的当前下标呢？

原因很简单：j代表的是为扩容前的下表，而上述既然表现出它比为扩容多一位，哪一位就恰恰好等于oldcap长度16，（这也是为什么hashmap扩容是扩两倍，都是环环相扣的）