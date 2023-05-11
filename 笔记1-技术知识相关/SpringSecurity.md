流程

### SpringSecurity 完整流程

SpringSecurity的原理其实就是一个过滤器链，内部包含了提供各种功能的过滤器。

![image-20230113215549944](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230113215549944.png)

核心过滤器

UsernamePasswordAuthenticationFilter: 负责处理我们在登录页面填写了用户名密码后的登录请求。

ExceptionTranslationFilter： 处理过滤器链中抛出的任何AccessDeniedExcep和AuthenticationException、

FilterSecuritylnterceptor: 负责处理权限校验的过滤器





#### 登录认证流程

![image-20230113221455879](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230113221455879.png)

  