### Lock 接口
##### Lock的成员方法
     
###### 1、void lock(); 
    获取锁，如果锁被暂用则一直等待
###### 2、void lockInterruptibly() throws InterruptedException;
    用该锁获得方式，如果线程在获取锁的阶段进入了等待阶段，那么可以中断此线程，先去做别的事请
###### 3、 boolean tryLock();
    注意返回值的类型是boolean，如果获取锁的时候锁被占用了就会返回false，否则返回true
###### 4、boolean tryLock(long time, TimeUnit unit) throws InterruptedException;
    比起tyrLock()就是给一个时间期限，保证等待参数的时间
###### 5、void unlock();
    释放锁
    
## ReentranLock（可重入锁） 实现了Lock接口

#### 1、构造器

    1、 无参构造器 默认是非公平锁
    public ReentrantLock() {
        sync = new NonfairSync();;//默认非公平锁
    }
    2、参数 boolean true：公平 false 不公平
    public ReentrantLock(boolean fair) {
        sync = fair ? new FairSync() : new NonfairSync();
    }
