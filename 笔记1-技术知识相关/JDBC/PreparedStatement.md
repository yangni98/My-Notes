## PreparedStatement

执行的SQL语句 中的参数 用？ 来表示 调用PreparedStatement对象的setXXX（）方法来设置这些参数

setXX（） 方法有两个参数 第一个参数是要设置的SQL语句中的参数的索引（从1开始）

第二个是设置SQL语句中的参数值

```java

package com.yn.jdbc.PreparedStatement;

import java.sql.*;

public class PStatement {
    public static void main(String[] args) throws SQLException {
        // 0.
        String username = "yn";
        String psd = "1324";


        //1.账号密码  连接地址
        String url ="jdbc:mysql://localhost:3307/jdbc_learn?serverTimezone=UTC";
        String name = "root";
        String password = "root";

        //2.获取连接
        Connection connection = DriverManager.getConnection(url, name, password);
        // sql语句
        String sql="select name,password from user where name=? and password=?";

        //3,获取PreparstatemtStatement
        PreparedStatement preparedStatement = connection.prepareStatement(sql);


        //4. 给？赋值
         preparedStatement.setString(1,username);
         preparedStatement.setString(2,psd);

        // 5. 得到结果
        ResultSet resultSet = preparedStatement.executeQuery();
        if (resultSet.next()){
            System.out.println("success");
        }else {
            System.out.println("false");
        }

        //6. 关闭
        resultSet.close();
        preparedStatement.close();
        connection.close();

    }
}
```