## HashMap
#### HashMap实现了Map接口 和继承了AbstractMap

## 成员属性

    1、static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16 （移位运算法1*2*2*2*2）
    DEFAULT_INITIAL_CAPACITY ：初始化容量，必须是2的幂 初始化是2的4次方
    
    2、static final int MAXIMUM_CAPACITY = 1 << 30;
    MAXIMUM_CAPACITY：最大容量，当隐式指定较高的值使用，
    由任何带参数的构造函数执行
    必须是2的幂 1 >> 30
    
    3、 static final float DEFAULT_LOAD_FACTOR = 0.75f;
    在构造函数中未指定时使用的加载因子
    
    4、  static final int TREEIFY_THRESHOLD = 8;
    TREEIFY_THRESHOLD :使用树而不是列表的bin计数阈值
    当想a中添加一个元素时，大于阈值则转换为数，这个值必须大于二，且至少为8
    
    5、 static final int UNTREEIFY_THRESHOLD = 6;
    容器计数器阈值用于取消对容器调整操作
    
    6、static final int MIN_TREEIFY_CAPACITY = 64;
    
    7、 transient Node<K,V>[] table;
    table 数组，在第一次使用的时候初始化，调整大小必要的，当分配时，长度总是2的幂
    
    7、transient Set<Map.Entry<K,V>> entrySet;
    entrySet;持有缓存的entry()
    
    8、int threshold; 调整大小的下一个大小值(容量*装载系数)。 capacity * loadfactor
    9、final float loadFactor; hash装载因子


### hashcode
      static final int hash(Object key) {
            int h;
            return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
       }
      返回key的hashcode值（散列码）
      
      public final int hashCode() {
            return Objects.hashCode(key) ^ Objects.hashCode(value);
       }
      
### 重新定义equasl方法

      public final boolean equals(Object o) {
                if (o == this)
                    return true;
                if (o instanceof Map.Entry) {
                    Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                    if (Objects.equals(key, e.getKey()) &&
                        Objects.equals(value, e.getValue()))
                        return true;
                }
                return false;
            }
        }

#### tableSizeFor(int cap) 

    static final int tableSizeFor(int cap) {
        int n = cap - 1;
        n |= n >>> 1;
        n |= n >>> 2;
        n |= n >>> 4;
        n |= n >>> 8;
        n |= n >>> 16;
        return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
    }
    
    返回给定目标容量的2倍幂。
    Returns a power of two size for the given target capacity.


## 构造器
    1、参数为初始值和装载因子
        public HashMap(int initialCapacity, float loadFactor) {
            if (initialCapacity < 0)
                throw new IllegalArgumentException("Illegal initial capacity: " +
                                                   initialCapacity);
            if (initialCapacity > MAXIMUM_CAPACITY)
                initialCapacity = MAXIMUM_CAPACITY;
            if (loadFactor <= 0 || Float.isNaN(loadFactor))
                throw new IllegalArgumentException("Illegal load factor: " +
                                                   loadFactor);
            this.loadFactor = loadFactor;
            this.threshold = tableSizeFor(initialCapacity);
        }
    2、参数初始容量
     public HashMap(int initialCapacity) {
            this(initialCapacity, DEFAULT_LOAD_FACTOR);
        }
      构造一个空的HashMap，初始值指定
        *容量和默认负载系数(0.75)。
        
     3、无参构造器
     初始容量为16 和转载因子为0.75
     public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
        }
        
        
        
#### get方法
public V get(Object key) {
        Node<K,V> e;
        return (e = getNode(hash(key), key)) == null ? null : e.value;
    }

    /**
     * Implements Map.get and related methods
     *
     * @param hash hash for key
     * @param key the key
     * @return the node, or null if none
     */
    final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            if ((e = first.next) != null) {
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }
    
first = tab[(n - 1) & hash]) != null 通过hash值定位到那个元素

