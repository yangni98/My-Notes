## 1.什么是springMVC？？  

springmvc是一个基于java的实现MVC设计模式的请求驱动类型的轻量级Web框架。

通过把 Model，View，Controller分离，将web层进行职责解耦，将复杂的web应用分成逻辑清晰的几部分，简化开发，减少出错，方便组内人员之间的配合。



## 2.SpringMVC的常用组件

DispatcherServlet

+ 是一种前端控制器，由框架提供。

  作用：统一处理请求和响应。除此之外还是整个流程控制的中心，由 DispatcherServlet 来调用其他组件，处理用户的请求

HandlerMapping

+ 处理器映射器，由框架提供。

  作用：根据请求的 url、method 等信息来查找具体的 Handler(一般来讲是Controller)

Handler(一般来讲是Controller)

+ 处理器，注意，这个需由工程师自己开发。

  作用：在 DispatcherServlet 的控制下，Handler对具体的用户请求进行处理

HandlerAdapter

+ 处理器适配器 ，由框架提供。

  作用：根据映射器找到的处理器 [Handler](https://so.csdn.net/so/search?q=Handler&spm=1001.2101.3001.7020) 信息，按照特定的规则去执行相关的处理器 Handler。

ViewResolver

+ 视图解析器，由框架提供。

  作用： ViewResolver 负责将处理结果生成 View 视图。 ViewResolver 首先根据逻辑视图名解析成物理图名，即具体的页面地址，再生成 View 视图对象，最后对 View 进行渲染将处理结果通过页面展示给用户。

view

视图，工程师自己开发

作用：View接口的职责就是接收[model](https://so.csdn.net/so/search?q=model&spm=1001.2101.3001.7020)对象、Request对象、Response对象，并渲染输出结果给Response对象。



## 3.SpringMVC工作流程

![img](https://img-blog.csdnimg.cn/75ec98a325394e748c10d1903f4ee419.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6bqm55Sw6YeM55qE5a6I5pyb6ICF5ZGA,size_17,color_FFFFFF,t_70,g_se,x_16)

（1）用户发送请求至前端控制器DispatcherServlet；
（2）DispatcherServlet收到请求后，调用HandlerMapping处理器映射器，请求获取Handler；
（3）处理器映射器根据请求url找到具体的处理器Handler，生成处理器对象及处理器拦截器(如果有则生成)，一并返回给DispatcherServlet；
（4）DispatcherServlet 调用 HandlerAdapter处理器适配器，请求执行Handler；
（5）HandlerAdapter 经过适配调用 具体处理器进行处理业务逻辑；
（6）Handler执行完成返回ModelAndView；
（7）HandlerAdapter将Handler执行结果ModelAndView返回给DispatcherServlet；
（8）DispatcherServlet将ModelAndView传给ViewResolver视图解析器进行解析；
（9）ViewResolver解析后返回具体View；
（10）DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）
（11）DispatcherServlet响应用户。

## 4.SpringMVC 设定重定向和转发？

（1）转发：在返回值前面加"forward:"，譬如"forward:user.do?name=method4"

（2）重定向：在返回值前面加"redirect:"，譬如"redirect:http://www.baidu.com"



### 5、 SpringMVC常用的注解有哪些？

@RequestMapping：用于处理请求 url 映射的注解，可用于类或方法上。用于类上，则表示类中的所有响应请求的方法都是以该地址作为父路径。

@RequestBody：注解实现接收http请求的json数据，将json转换为java对象。

@ResponseBody：注解实现将conreoller方法返回对象转化为json对象响应给客户。


## 6.SpringMVC拦截器实现

有两种写法，一种是实现HandlerInterceptor接口，另外一种是继承适配器类，接着在接口方法当中，实现处理逻辑；然后在SpringMvc的配置文件中配置拦截器即可：

```xml
<!-- 配置SpringMvc的拦截器 -->
<mvc:interceptors>
    <!-- 配置一个拦截器的Bean就可以了 默认是对所有请求都拦截 -->
    <bean id="myInterceptor" class="com.zwp.action.MyHandlerInterceptor"></bean>
 
    <!-- 只针对部分请求拦截 -->
    <mvc:interceptor>
       <mvc:mapping path="/modelMap.do" />
       <bean class="com.zwp.action.MyHandlerInterceptorAdapter" />
    </mvc:interceptor>
</mvc:interceptors>
```



## 7、SpringMvc怎么和AJAX相互调用的？
通过Jackson框架就可以把Java里面的对象直接转化成Js可以识别的Json对象。具体步骤如下 ：

（1）加入Jackson.jar

（2）在配置文件中配置json的映射

（3）在接受Ajax方法里面可以直接返回Object、List等，但方法前面要加@ResponseBody注解。
