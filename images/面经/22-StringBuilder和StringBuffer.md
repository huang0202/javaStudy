### StringBuffer

#####StringBuffer代码详解
```java

public final class StringBuffer extends AbstractStringBuilder{
    
    
    //transient 让某些修饰的成员变量不被序列化
    //在toString方法中被使用
    private transient char[] toStringCache;
    static final long serialVersionUID = 3388685877147921107L;
    
    //初始化长度默认是16
    public StringBuffer(){
        super(16);
    }
    
    // 传入参数初始化默认为capacity
    public StringBuffer(int capacity){
        super(capacity);
    }
    
    //构造函数传入一个字符串
    public StringBuffer(String str){
        super(str.length()+16);
        append(str);
    }
    //传入一个字符序列  
    public StringBuffer(CharSequence seq) {
        this(seq.length() + 16);
        append(seq);
    }


}
```

### 简介
    StringBuffer，由名字可以看出，是一个String的缓冲区，也就是说一个似于字符串缓冲区，
    和String不同的是，它可以被修改，而且线程是安全的。
    StringBuffer是线程安全的，因此如果有几个线程同时操作StringBuffer，对它来说也只是一个操作序列，所有操作串行发生。
    每一个StringBuffer都有一个容量，如果内容的大小不超过容量，StringBuffer就不会分配更大容量的缓存区，
    如果需要更大的容量，StringBuffer会自动增加容量。
    和StringBuufer类似的有StringBuilder，两者之间操作相同，不过StringBuilder不是线程安全的。
#### 原理
    StringBuffer继承了抽象类AbstractStringBuilder，在AbsrtactStringBuilder类中，有两个字段分别的是
    char[] 类型的value和和int类型的count，也就是说StringBuffer本质上是基于一个字符数组。

#### StringBuffer如何操作容量的改变
    1、首先StringBuffer有一个继承AbstractStringBuffer类的ensureCapacity方法
    @Override
    public synchronized void ensureCapacity(int minimumCapacity){
        if(minimumCapacity > value.length){
            //进行扩容
            expandCapacity(minimumCapacity)
        }
    }
    StringBuffer对其进行重写，直接调用父类的expandCapacity方法
    void expandCapacity(int minimumCapacity){
        int newCapacity = value.length * 2 + 2;
        if (newCapacity - minimumCapacity < 0)
            newCapacity = minimumCapacity;
        if (newCapacity < 0) {
            if (minimumCapacity < 0) // overflow
                 throw new OutOfMemoryError();
                 newCapacity = Integer.MAX_VALUE;
            }
        value = Arrays.copyOf(value, newCapacity);   
    }
    
    也就是说，value新的大小是value*2+2
    
    StringBuffer可以通过toString方法转化为String，他有一个私有字段toStringCache
    也就是一个缓存，用来保存上次调用toString的结果，如果value字符串序列发生改变，将会
    将他清空，toString代码如下
    
    @Override
    public synchronized String toString(){
        //这里的toStringCache是上次一toString的缓存
        //每一次对value的操作StringBuffer都会将其清空
        if(toStringCache == null){
            //表情对value进行过操作
            //对toStringCache重新赋值
            toStringCache = Arrays.copyOfRange(value, 0, count);
        }
        return new String(toStringCache,true);
    }

##  StringBuffer和String、StringBuilder的区别
#####速度上
    String<StringBuffer<StringBuilder
##### 安全上
    StringBuffer是线程安全的，StringBuilder线程不安全
####原因
    原因在于String每次改变都会涉及到字符数组的复制，而StringBuffer和StringBuilder直接在字符数组上改变；
    同时StringBuffer方法都被synchronized修饰，是线程安全的，而StringBuilder线程不安全，所以Stringbuilder快于StringBuffer
    
