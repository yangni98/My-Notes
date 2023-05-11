## 不同版本注意事项



**MySQL不同版本的注意事项** 

**1、驱动类driver-class-name**

 **MySQL 5版本使用jdbc5驱动，驱动类使用：com.mysql.jdbc.Driver**

 **MySQL 8版本使用jdbc8驱动，驱动类使用：com.mysql.cj.jdbc.Driver** 

**2、连接地址url**

 **MySQL 5版本的url： jdbc:mysql://localhost:3306/ssm** 

**MySQL 8版本的url： jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC** 

**否则运行测试用例报告如下错误： java.sql.SQLException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more**



### 1.创建工程

创建一个普通的maven工程

在pom文件里面导入需要的包

```xml
<dependencies>
<!-- Mybatis核心 -->
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis</artifactId>
<version>3.5.7</version>
</dependency>
<!-- junit测试 -->
<dependency>
<groupId>junit</groupId>
<artifactId>junit</artifactId>
<version>4.12</version>
<scope>test</scope>
</dependency>
<!-- MySQL驱动 -->
<dependency>
<groupId>mysql</groupId>
<artifactId>mysql-connector-java</artifactId>
<version>8.0.16</version>
</dependency>
</dependencies>
```



## 1.2 创建pojo实体类

```java
public class User {
   private Integer id;
   private String username;
   private String password;
   private Integer age;
   private String gender;
   private String email;
	.............................
        ........
        .//添加set和get方法 有参和无参构造
        
}
```



## 1.3 创建Mybatis的核心配置文件

**习惯上命名为mybatis-config.xml，这个文件名仅仅只是建议，并非强制要求。**

**将来整合Spring 之后，这个配置文件可以省略，**

**所以大家操作时可以直接复制、粘贴。 核心配置文件主要用于配置连接数据库**

**的环境以及MyBatis的全局配置信息 核心配置文件存放的位置是src/main/resources目录下**



## 1.4创建mapper接口

Mybatis中的mapper接口相当于以前的dao ，但是区别在于 mapper仅仅是接口 我们不需要提供实现类·

```java
package com.yn.mybatis.mapper;

public interface Usermapper {

    int insertUser();//返回值是int类型 是指被修改的行数
    			//insertUser是方法 后面再定义
}

```



## 1.5 创建MyBatis的映射文件

相关概念：ORM（Object Relationship Mapping） 对象关系映射

+ 对象：java的实体对象

+ 关系：关系型数据库

+ 映射：二者之间的关系

  

| Java概念 | 数据库概念 |
| -------- | ---------- |
| 类       | 表         |
| 属性     | 字段/列    |
| 对象     | 记录、行   |

1、映射文件的命名规则：

 表所对应的实体类的类名+Mapper.xml

 例如：表t_user，映射的实体类为User，所对应的映射文件为UserMapper.xml

 因此一个映射文件对应一个实体类，对应一张表的操作

 **MyBatis映射文件用于编写SQL，访问以及操作表中的数据** 

MyBatis映射文件存放的**位置是src/main/resources/mappers目录下** 

2、 MyBatis中可以面向接口操作数据，要保证两个一致：

 a>mapper接口的全类名和映射文件的命名空间（namespace）保持一致 

b>mapper接口中方法的方法名和映射文件中编写SQL的标签的id属性保持一致



#### 创建mapper文件 -----UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

下面是修改过的例子

```xml

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--和对应的接口连接  -->
<mapper namespace="com.yn.mybatis.mapper.UserMapper">

<!-- mapper接口和映射文件要要保持两个一致
    1，mapper接口的全类名和映射文件的namespace一致
    2，mapper接口中的方法的方法名要和映射文件的sql的id保持一致
-->

<!--    int insertUser();-->
    <insert id="insertUser">
--        下面是需要执行的sql
        Insert into t_user values (null ,'admin', '1234',18,'男','12345@qq.com');
    </insert>

</mapper>
```

#### 然后就是将User的映射文件引入到核心配置文件中（重要）

```xml
 <mappers>
        <package name="mappers/UserMapper.xml"/>
    </mappers>
```



### 全程预览

1.创建工程，导入配置，mybatis sql  junit

2.创建 数据库 表    ，并且对照数据库创建实体类  

3.创建 mybatis核心配置文件 在resources文件夹下 mybatis-config.xml

4.创建mappr接口   UserMapper（接口） 里面包含 返回值类型 和 方法

5.创建Mybatis映射文件  也是UserMapper的映射文件 里面写的主要是要执行的sql语句

6.将映射文件放入 mybatis的核心配置文件中





###  测试

```java
package com.yn.mybatis.test;

import com.yn.mybatis.mapper.UserMapper;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;

public class MyBatisTest {


    @Test
    public void test() throws IOException {
        // 获取核心配置文件的输入流
        final InputStream is  = Resources.getResourceAsStream("myvatis-config.xml");

        //获取sqlSessionBuilder对象
        SqlSessionFactoryBuilder sqlSessionBuilder = new SqlSessionFactoryBuilder();
//       获取SqlSessionFactory对象
        SqlSessionFactory sqlSessionFactory = sqlSessionBuilder.build(is);

        //获取sql的会话对象SqlSession 是Mybatis提供的操作数据库对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        
        //获取UserMapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);

        //调用mapper中的方法，实现添加用户信息的功能
        int result=mapper.insertUser();

        System.out.println("结果："+ result);

        //       事务提交
        sqlSession.commit();
        //关闭
        sqlSession.close();

    }

}

```







##  2.1 创建实体方法类

创建utils包 再 创建实体方法类  SqlSessionutil



```java

package com.yn.mybatis.utils;

import com.yn.mybatis.mapper.UserMapper;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.jupiter.api.Test;

import java.io.IOException;
import java.io.InputStream;

public class SqlSessionUtil {

    public static SqlSession getSqlSession(){
                SqlSession sqlSession=null;//4.1先声明sqlSession
        try {
            //1.获取核心配置文件的输入流
            InputStream is = Resources.getResourceAsStream("Mybatis-config.xml");
            //2.获取SqlSessionFactoryBuilder
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            //3.获取SqlSessionFactory对象
            SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
            //4.获取SqlSession对象。为sqLSession赋值
           sqlSession = sqlSessionFactory.openSession(true);//true是自动提交
        } catch (IOException e) {
            e.printStackTrace();
        }
        //5.返回sqlSession
        return sqlSession;
    }


    @Test
    public void testUpdate(){
    //1.先获取sqlSession对象
        SqlSession sqlSession = SqlSessionUtil.getSqlSession();
        //2.获取mapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //3.直接调用方法
        mapper.updateUser();
        //4.close();
        sqlSession.close();


    }


}

```

并且要去UserMapper接口和xml去写方法和sql语句

```java
  //修改用户信息
    int updateUser();
```



```xml
<!--    int updateUser();-->
    <update id="updateUser">
        update t_user set username='root', password='123' where id='2'
    </update>
```



## 2.2 添加删除方法



先写接口方法

```java

    //删除用户信息
    void deleteUser();
```

再写映射的mapper xml

```xml
<!--    void deleteUser();-->
    <delete id="deleteUser">
        delete from t_user where id='3'
    </delete>
```



然后再去实体类里面写方法

```java
   @Test
    public void testDelete(){
        //1.先获取sqlSession对象
        SqlSession sqlSession = SqlSessionUtil.getSqlSession();
        //2.获取mapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //3.直接调用方法
        mapper.deleteUser();
        //4.close();
        sqlSession.close();
    }
```

## 2.3查询

### 

```java
   //查询用户
    User getUserById();
```

```xml
<!--    resultType:设置结果集类型 即查询的数据要转换为java类型
        resultMap :自定义映射 ，处理多对一或一对多的映射关系-->
<!--    User getUserById();-->
    <select id="getUserById" resultType="com.yn.mybatis.pojo.User" >
        select * from t_user where id='2'
    </select>
```

```java
    @Test
    public void testGetUserById(){
        //1.先获取sqlSession对象
        SqlSession sqlSession = SqlSessionUtil.getSqlSession();
        //2.获取mapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //3.直接调用方法
        User user1 = mapper.getUserById();
        System.out.println(user1);
        //4.close();
        sqlSession.close();
    }

```

查询所有用户

```java
    //查询所有用户
    List<User> getAllUsers();
```

```xml
<!--    getAllUsers-->
    <select id="getAllUsers" resultType="com.yn.mybatis.pojo.User">
        select *  from t_user
    </select>
```

```java
    @Test
    public void testGetAllUser(){
        //1.先获取sqlSession对象
        SqlSession sqlSession = SqlSessionUtil.getSqlSession();
        //2.获取mapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //3.直接调用方法
        List<User> list = mapper.getAllUsers();

        list.forEach(System.out::println);
        //4.close();
        sqlSession.close();
    }

```





## 3 Mybatis核心配置文件

### 3.1environment 

```xml
    <!--设置连接数据库的环境-->
<!--    environments :配置连接数据库的环境
           属性：
                default：设置默认使用的环境的id-->
    <environments default="development">
<!--      environment: 设置一个具体的连接数据库的环境
            属性：
                id：设置环境的唯一标识，不能重复
                -->
        <environment id="development">
<!--            transactionManager：设置事务管理器
               属性：Type:设置事务管理的方式
                Type：JDBC/MANAGED
                JDBC:表示使用JDBC中原生的事务管理方式
                MANGED：被管理，-->
            <transactionManager type="JDBC"/>
<!--            dataSource：设置数据源
                     属性：
                            Type：设置数据源的类型
                            Type=”POOLED|UNPOOLED|JNDI“
                             POOLED:表示使用数据库连接池
                             UNPOOLED：表示不使用数据库连接池
                             JNDI：表示使用上下文中的数据源-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?
serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
```

## 5.Mybatis获取参数值的两种方式

