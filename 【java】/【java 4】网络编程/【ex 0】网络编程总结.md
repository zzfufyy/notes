#### 【ex 0】网络编程总结

--------

- TCP编程

  - 客户端

    1. 与对端建立Socket连接
  2. 创建输出流
    3. 输出流输出

    ```java
    int port = 9999;
    Socket socket = new Socket(InetAddress.getByName("127.0.0.1");, port);
    OutputStream os = socket.getOutputStream();
    os.write("你好，im zyw".getBytes(StandardCharsets.UTF_8));
    ```
    
  - 服务端

    1. 绑定服务端侦听端口
    2. 阻塞侦听
    3. 创建输入流，从socket接收数据
    4. 转成输出流输出

    ```java
    ServerSocket serverSocket = new ServerSocket(9999);
    Socket socket = serverSocket.accept();
    
    InputStream is = socket.getInputStream();
    
    // 管道流
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    byte[] buffer = new byte[1024];
    int len;
    while((len=is.read(buffer))!=-1){
      baos.write(buffer, 0,len);
    }
    System.out.println(baos.toString());
    ```

- UDP

  - 发送端

    1. 建立数据包socket（DatagramSocket）

    2. 数据包装成packet（包括ip和端口）

    3. socket发送packet

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

  - 接收端

    1. 绑定数据包socket侦听端口
    2. 数据包接收Packet（创建buffer数组初始化）存入数据
    3. socket接收packet 存入，创建的buffer Packet中
    4. packet.getData()

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

    

  