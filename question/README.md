# 面试问题

# 简介

顺手记录看到的面试问题以及答案

## hashMap

**1.HashMap的数据结构？**

hashmap采取数组+链表的数据结构，在遇到哈希冲突的时候采用链表结构来解决哈希冲突，jdk1.8后分成了两种情况，bucket中元素个数大于8的时候，自动转换为红黑树的结构。目的是因为链表的查询速度比较慢，元素越多越明显，改成红黑树是为了提高查询速度。

**2.HashMap是否线程安全？**

不安全  hashtable安全

**3.如果想使用线程安全的HashMap该如何做？**

 Collections的synchronizedMap() 方法使HashMap具有同步的能力

Map map = Collections.synchronizedMap(new HashMap());

或者使用ConcurrentHashMap

使用hashtable也可以

HashTable主要支持同步和但不允许null作为key和value，任一时刻只有一个线程能写Hashtable，即线程安全），因此也导致了 Hashtable 在写入时会比较慢。