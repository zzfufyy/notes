### JDBC

------------

#### 1. 什么是JDBC

- JAVA连接数据库

- 需要的jar包支持

  - java.sql
  - javax.sql
  - Mysql-connector-java   连接驱动

- 关于connection这里补充以下

  实际上connection是自动提交的。

  算事务提交。

  ```java
  connection.setAutoCommit(false);
  
  connection.prepareStatement(sql1).executeUpdate();
  connection.prepareStatement(sql2).executeUpdate();
  connection.prepareStatement(sql3).executeUpdate();
  
  connection.commit();
  ```

  

#### 2. 实例

- 基础实例

  ```java
  package com.zyw.test;
  
  import java.sql.*;
  
  public class TestJdbc {
      public static void main(String[] args) throws ClassNotFoundException, SQLException {
          String url = "jdbc:mysql://localhost:3306/jdbc? + " +
                  "useUnicode=true&characterEncoding=utf-8&autoReconnect=true&useSSL=false"
                  ;
          String username = "root";
          String password = "123456";
  
          // 加载驱动
          Class.forName("com.mysql.jdbc.Driver");
          // 连接数据库
          Connection connection = DriverManager.getConnection(url,username,password);
  
          // 向数据库 发送Sql对象statement
          Statement statement = connection.createStatement();
  
          String sql = "select * from users";
          ResultSet rs = statement.executeQuery(sql);
  
          while (rs.next()){
              System.out.println("id=" + rs.getObject("id"));
              System.out.println("id=" + rs.getObject("name"));
              System.out.println("id=" + rs.getObject("password"));
              System.out.println("id=" + rs.getObject("email"));
              System.out.println("id=" + rs.getObject("birthday"));
          }
          rs.close();
          statement.close();
          connection.close();
  
      }
  }
  
  
  ```

- 预编译

  ```java
  package com.zyw.test;
  
  import java.sql.*;
  
  public class TestJdbc {
      public static void main(String[] args) throws ClassNotFoundException, SQLException {
          String url = "jdbc:mysql://localhost:3306/jdbc? + " +
                  "useUnicode=true&characterEncoding=utf-8&autoReconnect=true&useSSL=false"
                  ;
          String username = "root";
          String password = "123456";
  
          // 加载驱动
          Class.forName("com.mysql.jdbc.Driver");
          // 连接数据库
          Connection connection = DriverManager.getConnection(url,username,password);
  
          // 向数据库 发送Sql对象statement
          String sql = "insert into users(id,name,password,email,birthday) values(?,?,?,?,?);";
          // 预编译(能输如参数)
          PreparedStatement prepareStatement = connection.prepareStatement(sql);
          prepareStatement.setInt(1, 4);
          prepareStatement.setString(2, "王6");
          prepareStatement.setString(3, "123456");
          prepareStatement.setString(4, "wn@qq.com");
          prepareStatement.setDate(5, new Date(new java.util.Date().getTime()));
  
  
          int i = prepareStatement.executeUpdate();
  
  
          prepareStatement.close();
          connection.close();
  
  
  
      }
  }
  
  ```

#### 3. 事务

- 要么都成功，要么都失败

- ACID原则，保证数据安全

  - Automicity  原子性

    一个事务的所有步骤，被看成一个动作，要么完成，要么失败。

  - Consitency 一致性

    事务开始前后，不能影响关系数据的完整性和业务逻辑上的一致性。

  - Isolation 隔离性

    事务之间不会相互影响，确保事务一个接一个的执行。

  - Durability 持久性

    一旦一个事务被提交，它应该持久保存，不会因为与其他操作冲突而取消这个事务。

- 事务操作

  - 开启事务
  - 事务提交
  - 事务回滚
  - 关闭事务

- 事务举例

  ```sql
  START TRANSACTION;
  UPDATE account 
  SET money = money - 100 
  WHERE
  	NAME = 'A';
  	UPDATE account 
  SET money = money + 100 
  WHERE
  	NAME = 'B';
  commit;	
  ```

  

