### 【extra 0】Mysql常见问题

---------------

- windows下安装mysql

  下载源码包，如：D:\mysql\mysql-5.7.29-winx64

  命令行进入该目录，下的bin文件夹。

  - 安装服务

    ```bash
    mysqld --install MYSQL5.7
    ```

  - 删除服务

    ```bash
    sc delete MYSQL5.7
    ```

  - 编辑my.ini文件

    ```ini
    [mysqld]
    
    explicit_defaults_for_timestamp=1
    basedir ="D:\\mysql\\MySQL Server 5.6"
    datadir ="D:\\mysql\\MySQL Server 5.6\\data"
    max_connection=200
    default-storage-engine=INNODB
    port = 3306
    
    sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 
    
    [mysql]
    default-character-set=utf8
    ```

    **注意：** sql_mode规定数据库规范

    如果不加这个，5.7默认为：

    ```sql
    ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
    ```

    这里  作出了较多的限制，在一些坑爹的sql中会出问题。

    所以一般会对全局设置变量进行修改。

    ```sql
    SET @@sql_mode = "STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
    SET @@global.sql_mode = ...
    ```

  - 删除data文件夹

  - 初始化mysql服务端

    ```bash
    mysqld --initialize  --default-file="配置文件路径"
    ```

  - 启动服务

    ```bash
    net start MYSQL5.7
    ```

  - 连接服务器

    第一次使用客户端工具连接，修改密码（有些特殊字符 cmd处理不了）

    ```bash
    mysql -uroot -P3357 -p123456
    ```

  - 修改密码

    ```sql
    use mysql;
    set password for root@localhost = password('123456');
    ```

  - 如果忘记密码

    ```bash
    mysqld --skpi-grant-tables
    mysql ##进入
    use mysql;
    update user set password=password("123") where user="root";
    flush privileges;  ## 刷新权限。
    ```

    