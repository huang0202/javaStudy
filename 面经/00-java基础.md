##ֵ���ݺ����ô���
    1��ֵ�����ǶԻ����ͱ������Եģ����ݵ��Ǹñ�����һ���������ı丱����ֵ��Ӱ��ԭ������
    2�����ô����ǶԶ�����Եģ����ݵ��Ǹö���ĵ�ַ��һ�����������Զ����ô��ݽ��в���
    ��ͬʱ�ı�ԭ���� 

```java

public class StringTest {
    public static void main(String[] args) {
        StringTest test = new StringTest();
        int i = 10;
        String str = new String("test");
        P huang = new P("huang");
        test.test(i,str);
        //���ô���
        test.fun(huang);

        System.out.println("main() i = " + i); //��� 10
        System.out.println("main() str = " + str); //��� test
        System.out.println("main() p = " + huang.value); //��� bo
    }

    public  void test(int i,String str){
        str = "testtest";
        i--;
        System.out.println("test() i=" + i); //��� 9
        System.out.println("test() str=" + str); //��� test
    }

    public  void fun(P p){
       p.value="bo";
       System.out.println("test()  p.value=" + p.value); //���bo

    }

}
class P{

    String value;
    public P(String value){
        this.value = value;
    }
}

```

## volatile�ؼ���
    volatile�ؼ�����������֤�����ԺͿɼ��ԡ����java���ڴ�ģ���йء�����������д�Ĵ��룬��һ���ǰ�������
    �Լ���д��˳����ִ�еģ�����������������cpuҲ������������������������Ϊ�˼�����ˮ�ߵ�������������ˮ������
    ������������Եģ����cpu��ִ��Ч�ʡ���Ҫһ����˳��͹�������֤����Ȼ����Ա�Լ�д�Ĵ��붼��֪���Բ��ԣ�
    ������happens-before�������о���volatile��������
    ��һ��������д�������ں������������Ķ������������Ե�ʵ����ͨ�������ڴ�����������֤�ġ�
    �ɼ��ԣ�����java�ڴ�ģ�ͷ�Ϊ���ڴ�͹����ڴ棬�����߳�A�����ڴ�ɱ�����ȡ�����Լ��Ĺ����ڴ棬���˼�1�Ĳ�����
    ����ʱû�н���������ֵˢ�µ����ڴ��У��߳�B��ȡ�Ļ���ԭ��ֵ��
    ����volatile�ؼ��ֵĴ������ɵĻ����뷢�֣�����һ��lockǰ׺ָ��
    
   
