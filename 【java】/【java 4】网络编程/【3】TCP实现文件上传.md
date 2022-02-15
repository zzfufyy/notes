#### 【3】TCP实现文件上传

----------

- 客户端

  ```java
  public class TcpFileClient {
      public static void main(String[] args) throws Exception{
          Socket socket = new Socket(InetAddress.getByName("127.0.0.1"),9000);
          // 创建输出流
          OutputStream os = socket.getOutputStream();
          // 读取文件
          FileInputStream fis = new FileInputStream(new File("zyw.jpg"));
          // 写卫门口am
          byte[] buffer = new byte[1024];
          int len;
          while((len=fis.read(buffer))!=-1){
              os.write(buffer,0,len);
          }
          // 通知服务器，我已经结束了
          socket.shutdownOutput(); // 我已经传输完了
  
          // 确定服务器接收完毕才能断开连接
          InputStream inputStream = socket.getInputStream();
          ByteArrayOutputStream baos = new ByteArrayOutputStream();
          byte[] buffer2 = new byte[1024];
          int len2;
          while((len2=inputStream.read(buffer2))!=-1){
              baos.write(buffer,0,len);
          }
          System.out.println(baos.toString());
  
          fis.close();
          os.close();
          socket.close();
      }
  }
  ```

- 服务端

  ```java
  
  public class TcpFileServer {
      public static void main(String[] args) throws  Exception{
          // 创建服务
          ServerSocket serverSocket = new ServerSocket(9000);
          // 阻塞式监听
          Socket socket = serverSocket.accept();
          // 输入流
          InputStream is = socket.getInputStream();
  
          // 文件输出
          FileOutputStream fos = new FileOutputStream(new File("receive"));
          byte[] buffer = new byte[1024];
          int len;
          while ((len=is.read(buffer))!=-1){
              fos.write(buffer,0,len);
          }
          // 通知客户端接收完毕了
          OutputStream os = socket.getOutputStream();
          os.write("我接受完毕了，可以断开".getBytes(StandardCharsets.UTF_8));
  
          os.close();
          fos.close();
          is.close();
          socket.close();
          serverSocket.close();
      }
  }
  
  ```

  