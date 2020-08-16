##值传递和引用传递
    1、值传递是对基本型变量而言的，传递的是该变量的一个副本，改变副本的值不影响原变量。
    2、引用传递是对对象而言的，传递的是该对象的地址的一个副本，所以对引用传递进行操作
    会同时改变原对象 

```java

public class StringTest {
    public static void main(String[] args) {
        StringTest test = new StringTest();
        int i = 10;
        String str = new String("test");
        P huang = new P("huang");
        test.test(i,str);
        //引用传递
        test.fun(huang);

        System.out.println("main() i = " + i); //输出 10
        System.out.println("main() str = " + str); //输出 test
        System.out.println("main() p = " + huang.value); //输出 bo
    }

    public  void test(int i,String str){
        str = "testtest";
        i--;
        System.out.println("test() i=" + i); //输出 9
        System.out.println("test() str=" + str); //输出 test
    }

    public  void fun(P p){
       p.value="bo";
       System.out.println("test()  p.value=" + p.value); //输出bo

    }

}
class P{

    String value;
    public P(String value){
        this.value = value;
    }
}

```

## volatile关键字
    volatile关键字是用来保证有序性和可见性。这跟java的内存模型有关。比如我们所写的代码，不一定是按照我们
    自己书写的顺序来执行的，编译器会做重排序，cpu也会做重排序，这样的重排序是为了减少流水线的阻塞，引起流水阻塞。
    比如数据相关性的，提高cpu的执行效率。需要一定的顺序和规则来保证。不然程序员自己写的代码都不知道对不对，
    所以有happens-before规则，其中就有volatile变量规则：
    对一个变量的写操作先于后面对这个变量的读操作，有序性的实现是通过插入内存屏障来不保证的。
    可见性：首先java内存模型分为主内存和工作内存，比如线程A从主内存吧变量读取到了自己的工作内存，做了加1的操作，
    但此时没有将变量最新值刷新到主内存中，线程B读取的还是原来值。
    加了volatile关键字的代码生成的汇编代码发现，会多出一个lock前缀指令
    
   
