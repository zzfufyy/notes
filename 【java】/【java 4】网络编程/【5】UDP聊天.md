#### 【5】UDP聊天

----------

* Sender

  ```java
  package com.zyw.socket;
  
  import java.io.BufferedReader;
  import java.io.InputStreamReader;
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  import java.net.InetSocketAddress;
  import java.nio.charset.StandardCharsets;
  
  public class UDPChatSender {
      public static void main(String[] args) throws Exception{
          DatagramSocket socket = new DatagramSocket(8888);
          BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
          while(true) {
              String data = reader.readLine();
              byte[] datas = data.getBytes(StandardCharsets.UTF_8);
              DatagramPacket packet = new DatagramPacket(datas, 0, datas.length, new InetSocketAddress("localhost", 6666));
              socket.send(packet);
              if(data.equals("bye")){
                  break;
              }
          }
          socket.close();
      }
  }
  
  ```

* Reciever

  ```java
  package com.zyw.socket;
  
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  
  public class UDPChatRecv {
      public static void main(String[] args) throws Exception{
          DatagramSocket socket = new DatagramSocket(6666);
  
          while(true){
              byte[] container = new byte[1024];
              DatagramPacket packet = new DatagramPacket(container,0,container.length);
              socket.receive(packet);
              // 断开连接
              byte[] data = packet.getData();
              String recvData = new String(data, 0, data.length);
              System.out.println(recvData);
              if(recvData.equals("bye")){
                  break;
              }
          }
      }
  }
  
  ```

  