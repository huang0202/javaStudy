###请问什么是IOC的DI?并且简要说明一下DI是如何实现的？
    考察点：控制反转

IOC叫控制反转，是Inversion of Controller的缩写，DI（Dependency Injection）叫依赖注入，是对Ioc更简单的诠释。
控制反转是把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。所谓的"控制反转"
就是对组件对象控制权的转移，从程序代码本身转移到了外部容器，由容器来创建对象并管理对象之间的依赖关系。
ioc体现了好莱坞原则-"Dont call me ,we will call you"。依赖注入的基本原则是应用组件不应该负责找资源或者
其他依赖的协作对象。配置对象的工作该由容器负责，查找资源的逻辑应该从应用组件的代码中抽取出来，交给容器来完成。
DI是对IOC更准确的描述，即组件之间的依赖关系由容器在运行期决定，形象的来说，即由容器动态的将某种依赖关系注入到组件中。

###springIOC原理是什么？如果你要实现IOC需要怎么做，请简单描述一下实现步骤

1、Ioc控制反转，这是spring的核心，贯穿始终。所谓IOC，对spring框架来说，就是由spring来负责控制对象的生命周期和对象间的关系。

2、Ioc的一个重点是在系统运行中，动态的向某一个对象提供他所需要的对象。这一点是通过DI（Dependency injection）依赖注入来实现的

3、实现IOC的步骤
定义用来描述bean的配置java类
解析bean的配置，，将bean的配置信息转化为上面的BeanDefinition对象保存在内存中，Spring中采用HashMap进行对象的存储，

遍历存放BeanDefinition的HashMap对象，逐条取出BeanDefinition对象，获取bean的配置信息，利用java反射机制来实例化对象，
将实例化后的对象保存在另外的一个Map中。

##### 依赖注入 接口注入、setter注入和构造器注入

###### 接口注入

```java
public class ClassA{
    private interfaceB clzB;
    
    public void doSomething(){
        Object obj = Class.forName(config.BImplementation).newInstance();
        clzB =(interfaceB)obj;
        clzB.doit();
    }    
......
}
```

我们根据预先在配置文件中设定的实现类的类名 (Config.BImplementation) ，动态加载实现类，并通过InterfaceB 强制转型后为 ClassA 所用。
这就是接口注入的一个最原始的雏形。
而对于一个ytpe1型的ioc容器而言，加载接口并创建其实列的工作由容器完成代码如下

````java
public class ClassA{
private interfaceB clzb;
    public Object doSomething(interfaceB b){
    clzb = b;
    return clzb.doit();
    }

}
````
在运行期间，InterfaceB实例将由容器提供

#####seter（设值）注入

```java
public class ClassA{
private interfaceB clzb;
public void setClzb(interfaceB b){
clzb = b;
}

}
```


#####构造器注入
    依赖关系是通过调用类的构造方法将其所需要的依赖关系注入其中

```java
public class DIByConstructor { 
private final DataSourcedataSource;
public DIByConstructor(DataSource ds) {
this.dataSource = ds;
}
……
}
```

##三种注入方式的比较
    1、接口注入
    接口注入模式因为历史比较悠久，在很多容器中已经得到应用，但由于其灵活性、易用性不如其他两种模式，因而在ioc中不被看好。
    2、setter注入
    对于习惯了传统javabean开发的程序员，通过setter设定依赖关系更加直观。
    如过依赖关系比较复杂，那么构造注入模式的构造函数会相当庞大，而此时设值注入模式则更为简洁。
    如果用到了第三方类库，可能需要要求我们组件提供一个默认的的构造函数，此时构造出入模式不适用。
    
    3、构造器注入
    在构造期间完成一个完整的、合法的对象。
    所有依赖关系在构造器函数中集中呈现。
    依赖关系在构造时由容器一次性设定，组件被创建之后处于相对“不变”的稳定状态。
    
