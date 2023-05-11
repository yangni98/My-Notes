## API

+ api就是java封装的类库  ----javase 所学的所有内容
+ 就是引入的包
+ java.lang 下面的包不需要手动引入
+ jdk官方提供的类库都是在jr.jar包
+ api 提供的应用程序编程接口



##  

## Object

### Object 有哪些方法

+ 1.在Object类中有一个无参构造方法
+ 2.Clone（）  克隆方法
+ 3.equals（Object obj） 比较两个对象是否相等
+ 4.finalize（） JVM垃圾回收机制
+ 5.getClass ()  —获取该对象的class
+ 6.hashCode（）  HashMap集合
+ 7.notify ， notifyAll（） ，wait（） ， wait
+ 8.toString（） 返回对象的字符串表达式
+ 9.多线程 synchronized  多线程之间的通讯



#### 直接继承和间接继承

+ 







#### toString

+ 对象重写了toString 主要输出成员属性值
+ 







#### equals

+ 使用equals 比较时 前面 如果为null.equals（比较） =====>报错

+ equals 比较两个对象值是否相同‘
+ == 比较两个对象的内存地址是否相同
+ 条件 :如果自定义的对象没有重写Object 父类的话
+ 则是在比较两个对象的  内存地址是否相同