### JDBC

-------------

#### 1. 概念

- 定义

  SUN公司为了而简化开发人员的操作。

  即对数据库的统一操作。

  提供了一个规范，俗称JDBC。

  <img src="imgs/截屏2021-08-07 下午4.56.24.png" alt="截屏2021-08-07 下午4.56.24" style="zoom:50%;" />

- 需要的jar包

  - java.sql
  - Javax.sql
  - 数据库驱动包

------------

#### 2. java程序

- 步骤

  - 加载驱动
  - 连接数据库DriverManager
  - 获得执行sql的对象Statement
  - 获得返回的结果集
  - 释放连接

- 示例

  ```java
  package com.zyw.lession01;
  
  import java.sql.*;
  
  public class JobFirstDemo {
      public static void main(String[] args) throws ClassNotFoundException, SQLException {
          // 1. 加载驱动
          Class.forName("com.mysql.cj.jdbc.Driver");
  
          // 2. 用户信息url
          String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf8&useSSL=true";
          String username = "root";
          String password = "123456";
  
          // 3. 连接成功，数据库对象
          Connection conn = DriverManager.getConnection(url, username, password);
  
          // 4. 执行sql的对象
          Statement st = conn.createStatement();
  
          // 5. 执行sql的对象，去执行sql
          String sql = "show tables";
          st.executeQuery(sql);
          ResultSet rs = st.executeQuery(sql);
  
          while(rs.next()){
              System.out.println(rs.getString(1));
          }
          // 6. 释放连接
          rs.close();
          st.close();
          conn.close();
      }
  }
  
  ```

- URL

  - mysql   3306

    Jdbc:mysql://主机地址:端口号/数据库名?参数1&参数2&参数3

  - oracle   1521

    Jdbc:oracle:thin:@localhost:1521:sid

- Statement

  执行SQL的对象

  ```java
  st.executeQuery(); // 查询
  st.execute();
  st.executeUpdate(); // 更新插入删除，返回受影响的行数
  ```

- PrepareStatement

  - 作用

    - 防止SQL注入

    - 并且效率更高

- Resultset

  ```java
  // 遍历指针
  resultSet.beforeFirst();  //移动到最前面
  resultSet.afterLast();
  resultSet.next();
  resultSet.previous();
  resultSet.absolute();
  ```

- 释放资源

----------------

#### 3. 工具类

- db.properties

  ```properties
  drvier=com.mysql.jdbc.Driver
  url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&userSSL=true
  username=root
  passsword=123456
  ```

- jdbcUtils

  ```java
  
  public class JdbcuTtils{
    private static String driver = null;
    private static String url  = null;
    private static String username = null;
    private static String password = null;
  	static {
      try{
      	InputStream in = JdbcUtils.class.getClassLoader();
        Properties prop = new Properties();
        prop.load(in);
        
        driver = prop.getProperty("driver");
        url = prop.getProperty("url");
       	username = prop.getProperty("username");
        password = prop.getProperty("password");
        
        // 1. 驱动只加载一次
        Class.forName(driver);
      }catch(Exception e){
        e.printStackTrace90；
      }
    }
    
    
    public static Connection getConnection(){
  		DriverManager.getConnection(url,username,password);
    }
    
    public static void release(Connection conn,Statement st, ResultSet rs){
      if(rs!=null){
        try{
          rs.close();
        }catch(SQLException e){
          e.printStackTrace();
        }
      }
      ...
    }
  }
  ```

- SQL注入

  - 举例

    比如加一个 `or 1=1`

    `and version()>0`

  - 解决办法

    **使用 PrepareStatement对象**

---------

#### 4. jdbc事务

- 代码

  ```java
  conn = JdbcUtils.getConnection();
  conn.setAutoCommit(false);
  String sql1 = "...";
  conn.prepareStatement(sql1);
  
  String sql2 = "...";
  conn.prepareStatement(sql2);
  
  st.executeUpdate();
  conn.commit();
  sout("成功");
  ```

----------

#### 5. 数据库连接池

- 概念

  - 原因：

    数据库连接到释放是十分浪费资源的。

  - 池化技术：

    准备一些预先的资源，过来就连接预先准备好。

    常用连接数。

    最小连接数。

    最大连接数（业务最高承载上限）

  - 实现技术：

    **编写接口实现DataSource接口**

    知名实现类：

    - DBCP
    - C3P0
    - Druid：阿里巴巴。

    使用了数据库连接池之后，在项目开发中，就不需要编写连接数据库的代码了。

  - DBCP

    - 需要的jar包

      ```java
      commons-dbcp-1.4.jar
      commons-pools-1.6.jar
      ```

    - 代码

      ```java
      InputStream in = JdbcUtils_DBCP.class.getLoader().getResourceAsStream("dbcpconfig.properties");
      Properties prop = new Properties();
      prop.load(in);
      
      // 创建
      DataSource dataSource = BasicDataSourceFactory.createDataSource(prop);
      
      
      
      public static Connection getConnection() throws SQLException(){
        return dataSource.getConnection();
      }
      ```

      