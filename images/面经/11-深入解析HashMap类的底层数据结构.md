# 深入解析HashMap类的底层数据结构、

### map接口
    * Map没有继承Collection接口，map提供key到value的映射。一个Map中不能包含相同的key，每一个key只能映射一个value
    * Map提供三种集合视图，map可以被当作一组key集合，一组value集合，或者一组key-value集合
### Hashtable类
    Hashtbale继承了map接口，实现一个key-value的哈希表，任何非空（non-null）的对象都可以座位key-或者value，
    添加数据使用put（key,value）,拿数据使用get(key)
