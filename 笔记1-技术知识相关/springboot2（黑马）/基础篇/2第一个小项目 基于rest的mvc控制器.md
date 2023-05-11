## 基于rest的 mvc控制器

 



### 第一步创建Controller

![image-20220930161907754](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20220930161907754.png)



## 写代码

```java
package com.itheima.controller;


import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

//Rest 模式
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping()
    public String getById(){
        System.out.println("运行成功》》》》》");
        return "springboot is running";
    }
    
}
```

## 注意：运行SpringBoot程序通过运行Application程序入口进行







## 创建项目时可以不通过spring官网创建 还可以通过阿里云创建

![image-20220930163730347](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20220930163730347.png)

http://satrt.aliyun.com

非常快速