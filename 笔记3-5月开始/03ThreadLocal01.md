# Threadlocal

简单来说，一个ThreadLocal在一个线程中是共享的，在不同线程之间又是隔离的（每个线程都只能看到自己线程的值）

ThreadLocal叫做线程变量，意思是ThreadLocal中填充的变量属于当前线程，该变量对其他线程而言是隔离的，也就是说该变量是当前线程独有的变量。ThreadLocal为变量在每个线程中都创建了一个副本，那么每个线程可以访问自己内部的副本变量。



![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-W7WJbbeK-1648006538639)(/assets/2021-10/tl1.png)]](https://img-blog.csdnimg.cn/7180cc567cba454ba1b12ad59a3396d0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA55Sw5Z-C44CB,size_20,color_FFFFFF,t_70,g_se,x_16)

![img](https://img-blog.csdnimg.cn/20201217201331591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA0NDUzMDE=,size_16,color_FFFFFF,t_70)



#### ThreadLocal的使用

一个ThreadLocal在一个线程中是共享的，在不同线程之间又是隔离的（每个线程都是只能看机到自己线程的值）

```java
public class _01ThreadLocal {
    private static ThreadLocal<Integer> la = new ThreadLocal<Integer>() {
        // 重写这个方法，可以修改“线程变量”的初始值，默认是null
        @Override
        protected Integer initialValue() {
            return 0;
        }
    };
    public static void main(String[] args) throws InterruptedException {

        //1号线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("一号线程set前："+la.get());
                la.set(1);
                System.out.println("一号线程set后："+la.get());
            }
        }).start();

        //二号线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("二号线程set前："+la.get());
                la.set(2);
                System.out.println("二号线程set后："+la.get());
            }
        }).start();

        //主线程睡1s
        Thread.sleep(1000);

        //主线程
        System.out.println("主线程的Threadlocal值："+la.get());
    }
}
```

结果：

一号线程set前：0
一号线程set后：1
二号线程set前：0
二号线程set后：2
主线程的Threadlocal值：0

##### 解释

每一个ThreadLocal实例就类似于一个变量名(每一个la就相当于是不同的变量名)

不同的ThreadLocal实例就是不同的变量名，它们内部会存在有一个值

ThreadLocal变量或者是线程变量，代表的就是ThreadLocal类的实例



程序结果重点看的是主线程输出的是0，如果是一个普通变量，在一号线程和二号线程中将普通变量设置为1和2，那么在一二号线程执行完毕后在打印这个变量，输出的值肯定是1或者2（到底输出哪一个由操作系统的线程调度逻辑有关）。但使用ThreadLocal变量通过两个线程赋值后，在主线程程中输出的却是初始值0。在这也就是为什么“一个ThreadLocal在一个线程中是共享的，在不同线程之间又是隔离的”，每个线程都只能看到自己线程的值，这也就是 ThreadLocal的核心作用：实现线程范围的局部变量。
————————————————



### 源码分析

原理：

每个Thread对象都有一个ThreadLocalMap，当创建一个ThreadLocal的时候，就会将ThreadLocal对象添加到该Map中，其中键值就是TreadLocal，值可以 是任意类型

之前说的是所有的常亮值或者是引用类型的引用都是保存在ThreadLocal实例中，但是实际上不是，这种说法只是让我们更好理解ThreadLocal变量这个概念。

向ThreadLocal存入一个值实际上是当前线程对象中的ThreadLocalMap存入一个值，实际上是当前线程对象中的ThreadLocalMap存入值，ThreadLocalMap可以理解成一个Map，而向这个Map存值的key就是ThreadLocal实例本身。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-rSZjitt2-1648006538642)(/assets/2021-10/tl4.png)]](https://img-blog.csdnimg.cn/fb715352533c4f379a2eacc547e777fa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA55Sw5Z-C44CB,size_20,color_FFFFFF,t_70,g_se,x_16)



ThreadLocal set赋值的时候首先会获取当前线程thread,并获取thread线程中的ThreadLocalMap属性。如果map属性不为空，则直接更新value值，如果map为空，则实例化threadLocalMap,并将value值初始化。







----------------------------------------------------

也就是说，想要存入的ThreadLocal中的数据实际上并没有存到ThreadLocal对象中去，而是以这个ThreadLocal实例作为key存到了当前线程中的一个Map中去了，获取ThreadLocal的值时同样也是这个道理。这也就是为什么ThreadLocal可以实现线程之间隔离的原因了。
————————————————

#### 内部类ThreadLocalMap

ThreadLocalMap是ThreadLocal的内部类，实现了一套自己的Map结构

ThreadLocalMap属性：

```java
        static class Entry extends WeakReference<ThreadLocal<?>> {
            Object value;
            Entry(ThreadLocal<?> k, Object v) {
                super(k);
                value = v;
            }
        }
        //初始容量16
        private static final int INITIAL_CAPACITY = 16;
        //散列表
        private Entry[] table;
        //entry 有效数量 
        private int size = 0;
        //负载因子
        private int threshold; 
```

ThreadLocaMap设置ThreadLocal变量

```java
private void set(ThreadLocal<?> key, Object value) {
    Entry[] tab = table;
    int len = tab.length;

    //与运算  & (len-1) 这就是为什么 要求数组len 要求2的n次幂 
    //因为len减一后最后一个bit是1 与运算计算出来的数值下标 能保证全覆盖 
    //否者数组有效位会减半 
    //如果是hashmap 计算完下标后 会增加链表 或红黑树的查找计算量 
    int i = key.threadLocalHashCode & (len-1);

    // 从下标位置开始向后循环搜索  不会死循环  有扩容因子 必定有空余槽点
    for (Entry e = tab[i];   e != null;  e = tab[i = nextIndex(i, len)]) {
        ThreadLocal<?> k = e.get();
        //一种情况 是当前引用 返回值
        if (k == key) {
            e.value = value;
            return;
        }
        //槽点被GC掉 重设状态 
        if (k == null) {
            replaceStaleEntry(key, value, i);
            return;
        }
    }
    //槽点为空 设置value
    tab[i] = new Entry(key, value);
    //设置ThreadLocal数量
    int sz = ++size;

    //没有可清理的槽点 并且数量大于负载因子 rehash
    if (!cleanSomeSlots(i, sz) && sz >= threshold)
        rehash();
}
```





———————————————————————————————————————————

### ThreadLocal与Synchronized区别

ThreadLocal<T>其实是与线程绑定的一个变量。ThreadLocal和Synchonized都用于解决多线程并发访问。

但是ThreadLocal与synchronized有本质的区别：

1、Synchronized用于线程间的数据共享，而ThreadLocal则用于线程间的数据隔离。

2、Synchronized是利用锁的机制，使变量或代码块在某一时该只能被一个线程访问。而ThreadLocal为每一个线程都提供了变量的副本

，使得每个线程在某一时间访问到的并不是同一个对象，这样就隔离了多个线程对数据的数据共享。

而Synchronized却正好相反，它用于在多个线程间通信时能够获得数据共享。

###### 一句话理解ThreadLocal，threadlocl是作为当前线程中属性ThreadLocalMap集合中的某一个Entry的key值Entry（threadlocl,value），虽然不同的线程之间threadlocal这个key值是一样，但是不同的线程所拥有的ThreadLocalMap是独一无二的，也就是不同的线程间同一个ThreadLocal（key）对应存储的值(value)不一样，从而到达了线程间变量隔离的目的，但是在同一个线程中这个value变量地址是一样的。

————————————————————————————————