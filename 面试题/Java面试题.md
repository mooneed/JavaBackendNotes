# 并发
为什么HashTable慢? 它的并发度是什么?那么ConcurrentHashMap并发度是什么?  
ConcurrentHashMap在JDK1.7和JDK1.8中实现有什么差别?JDK1.8解決了JDK1.7中什么问题?  
ConcurrentHashMap JDK1.7实现的原理是什么? 分段锁机制。  
ConcurrentHashMap JDK1.8实现的原理是什么? 数组+链表+红黑树，CAS。  
ConcurrentHashMap JDK1.7中Segment数(concurrencyLevel)默认值是多少? 为何一旦初始化就不可再扩容?  
ConcurrentHashMap JDK1.7说说其put的机制?  
ConcurrentHashMap JDK1.7是如何扩容的? rehash(注：segment 数组不能扩容，扩容是 segment 数组某个位置内部的数组 HashEntry<K,V>[] 进行扩容)  
ConcurrentHashMap JDK1.8是如何扩容的?   
tryPresizeConcurrentHashMap JDK1.8链表转红黑树的时机是什么? 临界值为什么是8?  
ConcurrentHashMap JDK1.8是如何进行数据迁移的? transfer  
XXX  
请先说说非并发集合中Fail-fast机制?  
再为什么说ArrayList查询快而增删慢?  
对比ArrayList说说CopyOnWriteArrayList的增删改查实现原理?   
COW基于拷贝再说下弱一致性的迭代器COWIterator原理是怎么样的?  
CopyOnWriteArrayList为什么并发安全且性能比Vector好?  
CopyOnWriteArrayList有何缺陷，说说其应用场景?  
