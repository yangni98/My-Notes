## 分页

 设置配置类  /   拦截器

```java
package com.yn.springnoot_ssmp.config;
import com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor;
import com.baomidou.mybatisplus.extension.plugins.inner.PaginationInnerInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MPConfig {
   @Bean
   public MybatisPlusInterceptor mybatisPlusInterceptor(){
       MybatisPlusInterceptor interceptor =new MybatisPlusInterceptor();
       interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
       return interceptor;
   }
}

```





测试类，执行

```java

    @Test
    void  testGetPage(){
        IPage page= new Page(1,5);
        bookMapper.selectPage(page,null);
    }
```







## 条件查询

```java
@Test
void  testGetBy(){

    QueryWrapper<Book> qw=new QueryWrapper<>();
    qw.like("name","B");
    bookMapper.selectList(qw);
}
```

