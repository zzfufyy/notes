#### 【1】IP地址、端口、通信协议

-----------------

* InetAddress类

  ```java
  InetAddress.getByName("127.0.0.1")；
  InetAddress ia = InetAddress.getByName("www.baidu.com");
  ia.getCanonicalHostName(); // 规范的名字
  ia.getHostAddress(); // host ip
  ia.getHostName(); // 域名  hostname
  
  ```

* 端口

  表示计算机上的一个程序的进程：

  - 不同的进程有不同的端口号。0-65535
  - 单个协议下，端口号不能冲突。tcp和udp都可以同时使用80这种，是可以的。

  - 端口号分类：

    - 公有端口号：0~1023

      - http：80
      - https：443
      - FTP：21
      - ssh：22
      - telent：23

    - 程序注册端口：1024~49151   分配给用户和程序

      - tomcat：8080
      - mysql：3306
      - oracle：1521

    - 动态、私有端口：49152~65535

      ```dos
      netstat -ano
      ```

* 通信协议

  - TCP：用户传输协议
    - 连接、稳定
    - 三次握手，四次挥手
    - 客户端，服务端
    - 传输完成、释放连接、效率低
  - UDP：用户数据报协议
    - 不连接、不稳定
    - 客户端、服务端：没有明确的界限
    - 不管有没有准备好，都可以发给你
    - 导弹
    - DDOS