# 1创建java Enterprise项目





在项目中创建一个新的srevlet

```
@WebServlet(value = "/login",loadOnStartup = 1)
```

是注解  跳转  到login    loadOnStartup=1 是优先级跳转



```
public class loginServlet extends HttpServlet {
    
}
```

继承 HttpServlet 接口



```
@WebServlet(value = "/login",loadOnStartup = 1)
public class loginServlet extends HttpServlet {

    @Override
    public void init() throws ServletException {
        super.init();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```

doPost 是进行post请求 登录用



前端代码



要包含在form表单里面

```
<form method="post" action="login">
```

方法 是post方法  action是login  不能加/



账号框和密码框 要写name 才能带上数据





重写 loginServlet的 init 初始方法

```java
SqlSessionFactory factory;
@SneakyThrows
@Override
public void init() throws ServletException {
    factory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsReader("mybatis-config.xml"));
}
```



然后在resources 配置  文件mybatis-config.xml



```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/study"/>
                <property name="username" value="${用户名}"/>
                <property name="password" value="${密码}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper class="com.example.mapper.UserMapper"/>
    </mappers>
</configuration>
```

//记住密码和账号要对





然后写数据库 简单点 就 id  账号  密码  

然后写实体类

写在entity里面

![image-20220907214646245](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20220907214646245.png)





用lombok写  方便

```
import lombok.Data;

@Data
public class User {
    int id;
    String username;
    String password;
}
```



然后写mapper 映射  并且记得把 mapper注册进配置文件里面



```java
package com.example.mapper;

import com.example.entity.User;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.annotations.Select;

public interface UserMapper {

    @Select("select * from users where username=#{username}and password=#{password}")
    User getUser(@Param("username") String username,@Param("password") String password);
}
```



配置里面注册

```
<mappers>
    <mapper class="com.example.mapper.UserMapper"/>
</mappers>
```











#  重定向



```
resp.sendRedirect("https://www.baidu.com");
```

sendRedirect方法.



# 请求转发



是服务器内部跳转机制

服务器内部进行转发  目的是 直接将本次请求转发给其他Servelet

并且由其他Servlet进行处理



![image-20220908153833989](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20220908153833989.png)
