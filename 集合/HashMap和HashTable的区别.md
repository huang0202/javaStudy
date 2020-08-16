## HashMap 和 Hashtable 的理解和区别
	HashTable 是java一开始发布时就提供的键值对映射的数据结构，而hashmap产生于JDK1.2，虽然hashtable比hashmap 出现早一些。但是现在hashtable 基本被废弃了，hashmap已经称为应用最为广泛的一种数据类型了，造成这个样的原因一方面是因为hashtable 是线程安全的，效率比较低，操作数据时会锁定整个hashtable ，对于线程安全方面，concurrentHashmap 做出了优化，锁定的是table的一个元素。

### 1.父类不同
	hashmap 是继承了AbstractMap类，而Hash Table 是继承自Dictionary（已被废弃）。不过他们都实现了map、cloneable（可复制）、Serializabel（可序列化） 这三个接口。

### null值问题
	HashTable 既不支持key为空同时也不支持value值为null，
	在hashmap中 null可以作为键，这样的键只有一个，可以又多个键对应值为null，当get方法返回null值时，可能hashmap中没有改键，或者存在该键他的value值为null。因此，在Hashmap中不能通过get方法来判断hashmap中是否存在某个键，而应该用containsKey（）方法来判断。

### 线程安全问题
	hashtable是线程安全的，在多线程并发的环境下，可能会产生死锁问题，使用hashmap时就必须要自己添加同步处理。

虽然hashmap是线程不安全的，但是他的效率比hashtable 要好很多，这样设计的是合理的，在我们日常使用中，大部分时间是单线程操作，hashmap把这部分操作解放出来了，当需要多线程操作的时候就可以使用线程安全的concrrenthashmap。
concurrenthashmap虽然也是线程安全的，但是他的效率要比hashtable 要高好多倍。因为concurrenthashmap 使用了分段锁。并不对整个数据进行锁定。

### 遍历的方式不同
	Hashtable、hashmap都使用了Iterator。而由于历史原因，Hashtable 还用了 Enumeration 的方法。
hashMap 、的Iterator 是fail-fast 迭代器。当有其他线程改变了hashmap的结构（添加、删除、修改元素），将会抛出conccurrentModificationException。不过，通过Iterator的remove（）方法


### 初始容量不同
	hashtable 的初始长度为11 每一次扩容都为之前的 2* n +1
而hashmap的初始长度为16，之后每次扩容为之后的两倍。创建时，如果给定了容量初始值，那么Hashtable 会直接使用你给定的值，而hashmap会将其扩充2的幂次方大小。

###  计算哈希值的方法不同
	为了得到元素的位置，首先需要根据元素的key来计算一个hash值，然后再用这个hahs值来计算得到最终的位置，hashtable 直接使用对象的hashcode。hashcode 是 jdk 根据对象的地址或者字符串或者数字算出来的int类型的数值，然后再使用除留余数来获得最终位置。然后除法运算时非常耗费时间的，效率比较低。
hashmap为了提高计算的效率，将哈希表的大小固定了为2的幂，这样在取模预算时，不需要做除法，只需套作为位运算，位运算比除法的效率要高很多。



















































