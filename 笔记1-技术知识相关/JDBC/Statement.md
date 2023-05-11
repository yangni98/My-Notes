### 用于执行静态SQl语句并返回其生成的结果的对象



建立连接以后，需要对数据库的进行访问 执行命令或者sql语句可以通过

1。Statement 

2. PreparedStatement
3. CallabelStatement



Statement对象 执行SQL 存在sql注入风险

```java
package com.yn.jdbc.Statement;

import com.mysql.cj.jdbc.Driver;

import java.sql.*;

public class Statement1 {
    public static void main(String[] args) throws SQLException {

        // 0.
        String username = "yn";
        String psd = "134";


        //1.账号密码  连接地址
        String url ="jdbc:mysql://localhost:3307/jdbc_learn?serverTimezone=UTC";
        String name = "root";
        String password = "root";

        //2.得到连接
        Connection connection = DriverManager.getConnection(url,name,password);

        //3.得到Statement
        Statement statement = connection.createStatement();


        //4 得到sql
        String sql = "select name,password from user where name='"
                +username+"' and password='"+psd+"'";

        ResultSet resultSet= statement.executeQuery(sql);

        if (resultSet.next()){
            System.out.println("success");
        }

        //5.关闭
        connection.close();
        resultSet.close();
        statement.close();
    }
}
```