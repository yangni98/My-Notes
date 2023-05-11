# HTTP协议

## 一 http协议特点

1.支持客户/服务器特点

2.简单快速： 客户向服务器请求服务时 只需要传送请求方法和路径 。 请求方法常有 GET POST 。每种方法规定了客户与服务器联系的类型不同。 由于HTTP协议简单，使得HTTP

服务器的程序规模小 因而通信速度快

3. 灵活 ：http允许传输任意类型的数据对象 传输的类型 由 Content-Type 加以标记
4. 无连接： 无连接是表示每次连接只需要处理一个请求 ，服务器处理完客户的请求，并收到客户的应答后，即断开连接 采用这种方式可以节省传输时间。
5. 无状态 ：HTTP协议是无状态协议 无状态协议对事物处理没有记忆能力 缺少状态意味着如果后续处理需要前面的学习 则它必须要重传 ，这样可能导致每次连接传送的数据量增大。在另一方面 在服务器不需要先前学习时它的应答就较快。

## 二Servlet

###  Servlet实现类

```xml
<!-- servlet及jstl标签库依赖的JAR配置 -->
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
  <version>3.1.0</version>
</dependency>
<dependency>
  <groupId>javax.servlet.jsp.jstl</groupId>
  <artifactId>jstl-api</artifactId>
  <version>1.2</version>
</dependency>
<dependency>
  <groupId>org.apache.taglibs</groupId>
  <artifactId>taglibs-standard-spec</artifactId>
  <version>1.2.1</version>
</dependency>
<dependency>
  <groupId>org.apache.taglibs</groupId>
  <artifactId>taglibs-standard-impl</artifactId>
  <version>1.2.1</version>
</dependency>
```



2.实现方法

```java
package com.yn.web.servlet;

import javax.servlet.*;
import java.io.IOException;

public class ServletDemo1 implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    //提供服务的方法
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello servlet");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```



3.配置

在web。xml中配置

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>

<!--  配置servlet-->
  <servlet>
    <servlet-name>demo1</servlet-name><!--  配置servlet名字-->
    <servlet-class>com.yn.web.servlet.ServletDemo1</servlet-class> <!--  配置servlet 全类名-->
  </servlet>
  
  <servlet-mapping><!--  配置servlet映射-->
    <servlet-name>demo1</servlet-name>
    <url-pattern>/demo1</url-pattern><!--  配置servlet资源路径-->
  </servlet-mapping>

</web-app>
```

4.启动tomcat

原理图

![](.\iamge\1.png)

1.当服务器接受到客户端浏览器请求后，会解析请求的URL路径，获取访问的Servlet的资源路径

2.查找web。xml文件是否对应的<url-pattern >标签体内容

3.如果有则会找到对应的全类名<servlet-class>

4.Tomcat 将全类名对应的字节码文件加载进内存Class.forname

5.创建对象 cls.newInstance();

6.调用方法---service



### Servlet 中的方法（生命周期）

实例对象由服务器创建

```java
//初始化方法
@Override
public voidpackage com.yn.web.servlet;

import javax.servlet.*;
import java.io.IOException;

//servlet中的方法
public class ServletDemo2 implements Servlet {
    //初始化方法
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("初始 化方法 init。。。。。");
    }

    // 获取Servletconfig对象
    @Override
    public ServletConfig getServletConfig() {
        return null;
    }


//    提供服务方法，执行多次
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("service.....");
    }
//获取servlet的一些信息，版本，作者等等
    @Override
    public String getServletInfo() {
        return null;
    }
//销毁方法，Servlet被正常关闭执行
    @Override
    public void destroy() {
        System.out.println("被销毁 destroy...");
    }
}
 init(ServletConfig servletConfig) throws ServletException {

}
```



周期：

在默认情况下，http服务器接受到对于当前Servlet接口实现类第一次请求时自动创建这个Servlet接口实现类

1. 被创建 ：执行init方法，执行一次

   ###### Servlet什么时候会被创建？

   + 默认情况下，第一次被访问时，Servlet被创建

   + 可以配置执行Servlet的创建时机

   + ```xml
       <servlet>
         <servlet-name>demo2</servlet-name><!--  配置servlet名字-->
         <servlet-class>com.yn.web.servlet.ServletDemo2</servlet-class> <!--  配置servlet 全类名-->
     <!--    指定创建时机
             第一次被访问时创建，值为负数
             服务器启动时创建，值为正数和0
             -->
         <load-on-startup>5</load-on-startup>
       </servlet>
     ```

Servletz只执行一次，说明servlet在内存中只存在一个对象，是单例的

多个用户同时访问时，可能存在一个线程安全问题

不能加锁（十分影响性能）

解决：尽量不要在servlet中定义成员变量，即使定义了成员变量也不要对其修改值。



2.提供服务：执行service方法执行多次

+ 每次访问，servlet都会被调用一次



3.被销毁：执行destroy方法，执行一次

+ servlet被销毁执行，服务器关闭时Servlet被销毁
+ 只有服务器正常关闭时，才会执行destroy方法





### Servlet3.0

支持注解配置，可以不需要web.xml,      			@WebServlet("/demo3")

```java
package com.yn.web.servlet;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;

@WebServlet("/demo3")
public class ServletDemo3 implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("servlket3.0");
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```





### httpServlet和Servlet

HttpServlet 指能够处理 HTTP 请求的 servlet，它在原有 Servlet 接口上添加了一些与 HTTP 协议处理方法，它比 Servlet 接口的功能更为强大。因此开发人员在编写Servlet时，通常应继承这个类，而避免直接去实现Servlet接口。

　　HttpServlet 在实现 Servlet 接口时，覆写了 service 方法，该方法体内的代码会自动判断用户的请求方式，如为 GET 请求，则调用 HttpServlet 的 doGet 方法，如为 Post 请求，则调用 doPost 方法。因此，开发人员在编写 Servlet 时，通常只需要覆写 doGet 或 doPost 方法，而不要去覆写 service 方法。
————————————————

```java
package com.yn.web.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo4")
public class HttpServlet04 extends HttpServlet {
    public HttpServlet04() {
        System.out.println("被创建！");
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
        System.out.println("doGet请求");
    }

    @Override
    protected long getLastModified(HttpServletRequest req) {
        return super.getLastModified(req);
    }

    @Override
    protected void doHead(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doHead(req, resp);
        System.out.println("doHead请求");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
        System.out.println("doPost请求");
    }

    @Override
    protected void doPut(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPut(req, resp);
        System.out.println("doPut请求");
    }

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);
        System.out.println("service1");
    }

    @Override
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        super.service(req, res);
        System.out.println("service2");
    }
}
```



### HttpServletResponse接口

1.HttpServletResponse接口来自于Servlet规范中，在tomcat中存在servlet-api.jar中

2.HttpServletResponse接口实现类由Http服务器负责提供

3.HttpServletResponse接口负责将doGet/doPost方法执行结果写入响应体中交给浏览器

4.通常将HttpServletResponse接口修饰的对象称为【响应对象】



###### 主要功能

+ 将执行结果以二进制形式写入到【响应体】

+ 设置响应头中的[content-type]属性值，从而控制浏览器使用

  对应编译器将响应体二进制数据编译为【文字，图片，视频，命令】

+ 设置响应头中的【location】属性将一个请求地址赋值给location，从而控制浏览器向指定服务器发送请求

+ 

+ ```java
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  
      System.out.println("doGet请求");
      String result ="hHHHHHHello!";
      //响应对象将结果写入到响应体中
      //通过响应对象，向Tomcat索要输出流
      PrintWriter out = resp.getWriter();
      out.write(result);
  }
  ```



### HttpServletRequest接口

1)HttpservletRequest接口来自于servlet规范中，在Tomcat中存在servlet-api.jar

2)HttpservletRequest接口实现类由Http服务器负责提供

3)HttpservletRequest接口负责在doGet/doPost方法运行时读取ttp请求协议包中信息



