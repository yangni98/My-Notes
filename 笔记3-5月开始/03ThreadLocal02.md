java官方文档中的描述： ThreadLocal类用来提供线程内部的局部变量，这种变量在多线程环境下访问（通过get和set方法访问） 时能保证各个线程的变量相对独立于其他线程的变量，

ThreadLocal实例通常来说都是private static类型的，用于关联程序的上下文

可以得知ThreadLocal作用是：提供线程内的局部变量，不同线程之间不会相互干扰，这种变量在线程的生命周期内作用，减少同一个线程内多个函数或组件之间一些公共变量传递的复杂度



————————————————————————————————

### ThreadLocal与Synchronized区别

ThreadLocal<T>其实是与线程绑定的一个变量。ThreadLocal和Synchonized都用于解决多线程并发访问。

但是ThreadLocal与synchronized有本质的区别：

1、Synchronized用于线程间的数据共享，而ThreadLocal则用于线程间的数据隔离。

2、Synchronized是利用锁的机制，使变量或代码块在某一时该只能被一个线程访问。而ThreadLocal为每一个线程都提供了变量的副本

，使得每个线程在某一时间访问到的并不是同一个对象，这样就隔离了多个线程对数据的数据共享。

而Synchronized却正好相反，它用于在多个线程间通信时能够获得数据共享。

###### 一句话理解ThreadLocal，threadlocl是作为当前线程中属性ThreadLocalMap集合中的某一个Entry的key值Entry（threadlocl,value），虽然不同的线程之间threadlocal这个key值是一样，但是不同的线程所拥有的ThreadLocalMap是独一无二的，也就是不同的线程间同一个ThreadLocal（key）对应存储的值(value)不一样，从而到达了线程间变量隔离的目的，但是在同一个线程中这个value变量地址是一样的。

|        | synchronized                                                 | ThreadLocal                                                  |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 原理   | 同步机制采用以“时间换空间”的方式，只提供了一份变量，让不同的线程排队访问 | ThreadLocal采用“以空间换时间”的方式，为每一个线程都提供了一份变量的副本，从而实现同步时访问而不相互干扰 |
| 侧重点 | 多个线程之间访问资源的同步                                   | 多线程中让每个线程之间的数据相互隔离                         |

