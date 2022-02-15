#### 【2】TCP程序聊天

-------------

* 程序

  客户端

  ```java
  package com.zyw.socket;
  
  import java.io.OutputStream;
  import java.net.Inet4Address;
  import java.net.InetAddress;
  import java.net.Socket;
  import java.net.UnknownHostException;
  import java.nio.charset.StandardCharsets;
  
  public class TcpClientDemo {
      public static void main(String[] args) throws Exception{
        InetAddress serverIP = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        Socket socket = new Socket(serverIP, port);
        OutputStream os = socket.getOutputStream();
        os.write("你好，im zyw".getBytes(StandardCharsets.UTF_8));
        socket.send(os);
      }
  }
  
  ```
  
  服务端
  
  ```java
package com.zyw.socket;
  import java.io.ByteArrayInputStream;
    import java.io.ByteArrayOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.net.ServerSocket;
    import java.net.Socket;
  
    public class TcpServerDemo {
        public static void main(String[] args) throws IOException {
          ServerSocket serverSocket = null;
        Socket socket = null;
        InputStream is = null;
        ByteArrayOutputStream baos = null;
          try {
            serverSocket = new ServerSocket(9999);
            socket = serverSocket.accept();
            is = socket.getInputStream();
    
            // 管道流
            baos = new ByteArrayOutputStream();
            byte[] buffer = new byte[1024];
            int len;
            while((len=is.read(buffer))!=-1){
                baos.write(buffer, 0,len);
            }
            System.out.println(baos.toString());
    
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            // 关闭资源
            baos.close();
            is.close();
            socket.close();
            serverSocket.close();
        }
    }
        }            
  ```

  ```
  
  
  ```