### 配置文件 properties 是springboot原生的配置文件

更改服务端口

```
server.port=
```

优先级：properties最高

​				yml 

​				yaml 最低

不同配置文件中相同配置按照加载优先级相符覆盖，不同配置文件中不同配置全部保留

![image-20221012112633660](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221012112633660.png)



读取Yml数据

```java
  //读取yaml数据中的单一数据
    @Value("${country}")
    private  String country1;

```



![image-20221012152049138](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221012152049138.png)

