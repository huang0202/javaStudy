# 集合框架 collection

## 定义
    集合和数组类似，只不过集合种的数据量可以动态的改变
    
### 集合
    1、List集合:存放的数据可以重复，并且有顺序 实现类：{ArrayList，LinkedList}
    2、Set集合：存放的数据无序不可重复
    3、Map集合：双列型，存放数据无序，key不可以重复，value可以重复 


### ArrayList
   
###### 1、底层是Object数组

###### 2、成员变量
    1、private static final int DEFAULT_CAPACITY = 10;
    DEFAULT_CAPACITY ：默认的capacity 初始化的时候默认长度为10
    
    2、 private static final Object[] EMPTY_ELEMENTDATA = {};
    EMPTY_ELEMENTDATA：用于空实例的共享空数组实例
    
    3、private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    DEFAULTCAPACITY_EMPTY_ELEMENTDATA
    用于默认大小的空实例的共享空数组实例
    我们将其与EMPTY_ELEMENTDATA 区分开，便知道何时膨胀，膨胀多少，添加第一个元素
    
    4、 transient Object[] elementData; 
    存储ArrayList元素的数组缓冲区
    ArrayList的容量是找个数组的缓冲的长度，
    empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
    将在添加第一个元素是扩张为 DEFAULT_CAPACITY，默认是10；
    
    5、 private int size;
    size：ArrayList的大小（包含元素的数量）
    
###### 3、构造器
   
    1、无参构造器
      public ArrayList() {
            this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
        }
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    transient Object[] elementData;
    private static final int DEFAULT_CAPACITY = 10;
    使用无参构造器初始化一个数组的大小为10
    
    1、将initialCapacity作为参数传递
      public ArrayList(int initialCapacity) {
            if (initialCapacity > 0) {
                this.elementData = new Object[initialCapacity];
            } else if (initialCapacity == 0) {
                this.elementData = EMPTY_ELEMENTDATA;
            } else {
                throw new IllegalArgumentException("Illegal Capacity: "+
                                                   initialCapacity);
            }
        }
    就会初始化一个 this.elementData = new Object[initialCapacity];
    就会初始化一个长度为initialCapacity的object数组   
    
    3、扩容方法 grow()
       private void grow(int minCapacity) {
            // overflow-conscious code
            int oldCapacity = elementData.length;
            //newCapacity = oldCapacocity + (oldCapacity >> 1)
            //这里的>> 右移一位，相当于除以二，加上原来的 相当扩容为之前的1.5
            int newCapacity = oldCapacity + (oldCapacity >> 1);
            if (newCapacity - minCapacity < 0)
                newCapacity = minCapacity;
            if (newCapacity - MAX_ARRAY_SIZE > 0)
                newCapacity = hugeCapacity(minCapacity);
            // minCapacity is usually close to size, so this is a win:
            最后使用Arrays.copyOf方法，将原来的数据复制到扩容后长度的数组中，扩容的操作完成！
            elementData = Arrays.copyOf(elementData, newCapacity);
        }
    4.get和remove方法
    get(int index) 通过下表查询
    remove(int index) 通过下表删除
    remove(Object o) 
    
    public boolean remove(Object o) {
            if (o == null) {
                for (int index = 0; index < size; index++)
                    if (elementData[index] == null) {
                        fastRemove(index);
                        return true;
                    }
            } else {
                for (int index = 0; index < size; index++)
                    if (o.equals(elementData[index])) {
                        fastRemove(index);
                        return true;
                    }
            }
            return false;
        }
        


    

