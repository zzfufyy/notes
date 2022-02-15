#### 【4】UDP消息发送

-----------

* 概述

  UDP，无连接。

  其实是没有客户端、服务端的概念的。

  他并没有建立连接就发送了数据。

  TCPsocket  必须绑定端口号，如果建立连接失败，会抛出。

  UDPsocket 是用packet实现的。

* client

  ```java
  
  // 建立socket
  DatagramSocket socket = new DatagramSocket();
  // 建包
  InetAddress localhost = InetAddress.getByName("localhost");
  int port = 8080;
  String msg = "你好啊，服务器";
  DatagramPacket packet = new DatagramPacket(msg.getBytes(StandardCharsets.UTF_8),0,msg.getBytes(StandardCharsets.UTF_8).length,localhost, port);
  // 发包
  socket.send(packet);
  socket.close();
  
  ```

* server

  ```java
  // 开放端口
  DatagramSocket socket = new DatagramSocket(8080);
  byte[] buffer = new byte[1024];
  DatagramPacket packet = new DatagramPacket(buffer, 0, buffer.length);
  // 阻塞接收，接收到也不会停止
  socket.receive(packet);
  System.out.println(packet.getAddress().getHostAddress());
  System.out.println(new String(packet.getData(),0,packet.getLength()));
  socket.close();
  ```

  

