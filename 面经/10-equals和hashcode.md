## equals()方法详解

#### equals()方式是用来判断其他的对象是否和该对象相等

```java
public  boolean equals(Object obj){
     return (this == obj)
     }      
````
    很明显是对两个对象的地址进行比较（及比较的是引用是否相同）。但是我们知道String、Math、Integer
    Double等等这些封装类在使用equals（）方法是，已经覆盖了object类的equals()方法
### 比如在String类中的equals()

```java

public class String{
    public boolean equals(Object anObject){
        if(this == anObject){
        return true;
        }
        if(anObject instanceof String){
            String anotherString = (String)anObject;
            int n = count;
            if(n == anotherString.count){
             char v1[] = value;
             char v2[] = anotherString.value;
             int j = offset;
             int i = anotherString.offset;
             while (n -- != 0){
                if (v1[i++] != v2[j++])  
                  return false;
                }
             return ture;
            }
        }
    return false;
    }   

}
```

## hashcode()方法详解
##### hashcode方法是给对象返回一个hashcode 的值，该方法用于hash tables，例如HashMap.

### 性质
    1.在一个java应用的执行期间，如果一个对象提供给equals作比较的信息没有被修改的话，该对象多次调用hashCode()方法返回的始终是一个interger
    2.如果两个对象根据equals(object)的方法是相等的，那么调用二者的hashcode产生的是同一个integer结构
    3.并不要求根据equals()方法不相等的对象，调用二者的hashcode方法必须产生不同的integer的结果
    程序员应该意识到对于不同的对象产生不同的integer结果
###### public native int hashCode();

###### 说明是一个本地方法，它的实现是根据本地机器相关的。当然我们可以在自己写的类中覆盖hashcode()方法，，比如String、Inteeger、Double等这些类都是覆盖了hashcode()方法。比如   String类下的hashcoed 的方法定义
    
```java

public class String{
    public int hashcode(){
        int h = hash;
        if(h == 0){
        int off = offset;
        char[] val = value;
        int len = count;
        
        for(int i = 0; i < len; i++) {
           h = 31 * h + val[off++];  
        }
        hash = h;   
        }
        return h;
    }
    
}
```

    想要弄明白hashcode的作用，必须要先知道java中的集合
    总的来说，java中的集合（collection）有两类，一是list、二是set，前者集合内元素是有序的，元素可以重复，后者元素是无序的，但是元素不可以重复。
    这里就有一个问题，保证两个元素不重复应该用什么依据来判断
    这个就是equals方法了，但是每添加一个元素就检查一次，当s集合中有很多元素的时候，后面添加到集合中的元素就需要经过很多次的比较，
    也就是说，如果集合中有1000个元素，那么在添加一个元素，就要调用1001次的equals方法，这样就效率很低
    于是，java采用hash表的原理，哈希算法也成为散列算法，是将依据特定的算法直接指定到一个地址上，初学者可以简单理解，
    hashcode方法实际上返回的是对象存储的物理地址（实际上可能不是） 
###### 简而言之在集合查找时，hashcode能大大降低对象的比较次数，提高查询效率！
    java对象的equals方法和hashcode方法是这样规定的
    
    1、相等（相同）的对象对象必须具有相等的哈希码（或者散列码）
    2、如果两个对象的hashcode相同的，但他们并不一定相同。

#### java对于equals方法和hashCode方法是这样规矩的；
    
    1、如果两个对象相同，那么对于他们的hashcode值一定相同；
    
    2、如果两个对象的hashcode相同，它们并不一定相同（这里说的对象相同指的是equasl方法比较）
    
#### 下面以HashSet为例进行分析，，我们都知道，在HashSet中不允许出现重复的现象，元素的位置也不确定，在hashset中又是怎么样判断元素是否重复呢
    在java集合中，判断两个对象是否相等的规则是
        1、判断两个对象的hashcode是否相等
            如果不相等，认为这两个对象不相等，完毕
            如果相等转
        2、判断两个对象用equals运算是否相等
            如果不相等，认为着两个对象不相等
            如果相等，则认为着两个对象相等

