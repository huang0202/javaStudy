### StringBuffer

#####StringBuffer�������
```java

public final class StringBuffer extends AbstractStringBuilder{
    
    
    //transient ��ĳЩ���εĳ�Ա�����������л�
    //��toString�����б�ʹ��
    private transient char[] toStringCache;
    static final long serialVersionUID = 3388685877147921107L;
    
    //��ʼ������Ĭ����16
    public StringBuffer(){
        super(16);
    }
    
    // ���������ʼ��Ĭ��Ϊcapacity
    public StringBuffer(int capacity){
        super(capacity);
    }
    
    //���캯������һ���ַ���
    public StringBuffer(String str){
        super(str.length()+16);
        append(str);
    }
    //����һ���ַ�����  
    public StringBuffer(CharSequence seq) {
        this(seq.length() + 16);
        append(seq);
    }


}
```

### ���
    StringBuffer�������ֿ��Կ�������һ��String�Ļ�������Ҳ����˵һ�������ַ�����������
    ��String��ͬ���ǣ������Ա��޸ģ������߳��ǰ�ȫ�ġ�
    StringBuffer���̰߳�ȫ�ģ��������м����߳�ͬʱ����StringBuffer��������˵Ҳֻ��һ���������У����в������з�����
    ÿһ��StringBuffer����һ��������������ݵĴ�С������������StringBuffer�Ͳ��������������Ļ�������
    �����Ҫ�����������StringBuffer���Զ�����������
    ��StringBuufer���Ƶ���StringBuilder������֮�������ͬ������StringBuilder�����̰߳�ȫ�ġ�
#### ԭ��
    StringBuffer�̳��˳�����AbstractStringBuilder����AbsrtactStringBuilder���У��������ֶηֱ����
    char[] ���͵�value�ͺ�int���͵�count��Ҳ����˵StringBuffer�������ǻ���һ���ַ����顣

#### StringBuffer��β��������ĸı�
    1������StringBuffer��һ���̳�AbstractStringBuffer���ensureCapacity����
    @Override
    public synchronized void ensureCapacity(int minimumCapacity){
        if(minimumCapacity > value.length){
            //��������
            expandCapacity(minimumCapacity)
        }
    }
    StringBuffer���������д��ֱ�ӵ��ø����expandCapacity����
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
    
    Ҳ����˵��value�µĴ�С��value*2+2
    
    StringBuffer����ͨ��toString����ת��ΪString������һ��˽���ֶ�toStringCache
    Ҳ����һ�����棬���������ϴε���toString�Ľ�������value�ַ������з����ı䣬����
    ������գ�toString��������
    
    @Override
    public synchronized String toString(){
        //�����toStringCache���ϴ�һtoString�Ļ���
        //ÿһ�ζ�value�Ĳ���StringBuffer���Ὣ�����
        if(toStringCache == null){
            //�����value���й�����
            //��toStringCache���¸�ֵ
            toStringCache = Arrays.copyOfRange(value, 0, count);
        }
        return new String(toStringCache,true);
    }

##  StringBuffer��String��StringBuilder������
#####�ٶ���
    String<StringBuffer<StringBuilder
##### ��ȫ��
    StringBuffer���̰߳�ȫ�ģ�StringBuilder�̲߳���ȫ
####ԭ��
    ԭ������Stringÿ�θı䶼���漰���ַ�����ĸ��ƣ���StringBuffer��StringBuilderֱ�����ַ������ϸı䣻
    ͬʱStringBuffer��������synchronized���Σ����̰߳�ȫ�ģ���StringBuilder�̲߳���ȫ������Stringbuilder����StringBuffer
    
