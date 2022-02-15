### Servlet

-----------

#### 1. 简介

- Servlet是sun公司开发的动态web的一门技术
- API提供的一个接口Servelt：
  - 编写一个类，实现Servlet接口
  - 把开发号的java类部署到web服务器中

#### 2. 修改web.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://java.sun.com/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                                 http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
           version="2.5">

  </web-app>
  ```

#### 3. Helloservlet

- 构建一个maven项目

- 父子工程

  - 父项目pom.xml中会多一个

    ```xml
    <modules>
        <module>servlet-01</module>
    </modules>
    ```

    

  - 子项目pom.xml中会多一个

    ```xml
    <parent>
        <artifactId>javaweb-01-maven</artifactId>
        <groupId>com.zyw</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <artifactId>servlet-001</artifactId>
    ```


#### 4. 编写Servlet映射

- 为什么需要映射

  我们写的是java程序，但是需要通过浏览器访问

  而浏览器需要连接web服务器，

  所以我们需要在web服务中注册我们写的servlet。

  给一个浏览器能够访问的路径。

- 编写映射

  在web.xml中

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                                http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
    
          <!-- 注册servlet        -->
          <servlet>
              <servlet-name>hello</servlet-name>
              <servlet-class>com.zyw.servlet.HelloServlet</servlet-class>
          </servlet>
    
    			<!-- servlet的请求路径        -->
          <servlet-mapping>
              <servlet-name>hello</servlet-name>
              <url-pattern>/hello</url-pattern>
          </servlet-mapping>
  </web-app >
  ```

  

#### 5. 编写Servlet

Servlet接口在Sun公司有两个实现类：

- HttpServlet
- GenericServlet

```java
package com.zyw.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
public class HelloServlet extends HttpServlet {

		// post方法
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);

    }
  	// get方法
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("进入doget");
        // ServletOutputStream outputStream = resp.getOutputStream();
        PrintWriter writer = resp.getWriter();
        writer.print("Hello,Servlet");
    }
}

```



#### 6. tomcat

idea中配置tomcat，需要配置到webapp目录。

启动即可

#### 7. servlet原理

- ServletContext

  web容器启动的时候，为每个web程序都创建一个对应额servletContext。

  它代表了当前的web应用

  作用：

  - 共享数据

    我在这个Servlet中保存的数据，可以在另外一个Servlet中拿到

    ```java
    // HelloServlet.java
    // doGet方法中
    ServletContext context = this.getServletContext();
    String username = "秦疆";
    context.setAttribute("username", username); // 将一个数据保存在Servlet中
    
    // GetServlet.java
    // doGet方法中
    ServletContext context = this.getServletContext();
    String name = (String) context.getAttribute("username");
    System.out.println(name);
    
    //  context 使得同一个web程序中不同servlet可以通信
    
    ```

#### 8. HttpServletResponse 和 HttpServletRequest

​	web服务器接收到客户端http请求，

​	针对这个请求，

​	分别创建一个代表请求的HttpServletRequest对象

​	代表响应的一个HttpServletResponse对象。

- HttpServletResponse

  给客户端响应一些信息。

  set系列方法。

  ```java
  void sendError(int var1, String var2) throws IOException;
  
  void sendError(int var1) throws IOException;
  
  void sendRedirect(String var1) throws IOException;
  
  void setDateHeader(String var1, long var2);
  
  void addDateHeader(String var1, long var2);
  
  void setHeader(String var1, String var2);
  
  void addHeader(String var1, String var2);
  
  void setIntHeader(String var1, int var2);
  
  void addIntHeader(String var1, int var2);
  
  void setStatus(int var1);
  ```

- HttpServletRequest

  获取客户端请求过来的参数。

  get系列方法。
  
  HTTP请求中所有信息会被封装到HttpServletRequest
  
  通过这个Request的方法，获得客户端的所有信息。
  
  ```java
  
  // 获取get表单username
  
  req.setCharacterEncoding("utf-8");
  resp.setCharacterEncoding("utf-8");
  String username = req.getParameter("username");
  String password = req.getParameter("password");
  String[] hobbys = req.getParameterValues("hobbys")
  
  sout Arrays.toString(hobbys);
  
  // 通过请求转发
  req.getRequestDispatcher(req.getContextPath() + "/success.jsp").forward(req.resp);
  
  ```
  
  JSPpost表单
  
  ```html
  <div style="text-align:center">
    <from action="${pageContext.request.contextPath}/login" method="post">
    用户名:<input type="text" name="username"> <br>
      密码:<input type="text" name="password"> <br>
      爱好:
      <input type="checkbox" name="hobbys" value="女孩">女孩
      <input type="checkbox" name="hobbys" value="代码">代码
      <input type="checkbox" name="hobbys" value="唱歌">唱歌
      <input type="checkbox" name="hobbys" value="电影">电影
      <br>
      <input type="submit">
    </from>
  </div>
  ```
  
  



#### 9. 实例1 - 下载文件

1. 获取下载文件路径
2. 文件名
3. 想办法让浏览器支持下载我们需要的东西
4. 获取下载文件的输入流
5. 创建缓冲区
6. 获取outputStream对象
7. 将FileoutputStream 流写入buffer缓冲区
8. 使用outputstream缓冲区中的数据输出到客户端

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  String realPath = "/Users/admin/IdeaProjects/javaweb-01-maven/servlet-002/src/main/resources/1.jpeg";
  System.out.println("下载路径"+realPath);

  // 获取文件名
  String fileName = realPath.substring(realPath.lastIndexOf("\\")+1);

  // 设置响应头
  resp.setHeader("Content-Disposition","attachment;filename="+fileName);
  FileInputStream in = new FileInputStream(realPath);

  // 缓冲区
  int len = 0;
  byte[] buffer = new byte[1024];

  ServletOutputStream out = resp.getOutputStream();

  while((len =  in.read(buffer))>0){
    out.write(buffer, 0, len);
  }
  in.close();
  out.close();
}
```

#### 10. 实例2 - 验证码

1. 前端实现
2. 后端实现

```java
package com.zyw.servlet;

import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

public class ImageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 浏览器3s刷新
        resp.setHeader("refresh","3");

        // 在内存中创建图片
        BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);

        //  得到图片
        Graphics2D g = (Graphics2D) image.getGraphics();
        g.setColor(Color.white);
        g.fillRect(0,0,80,20);

        // 给图片写数据
        g.setColor(Color.BLUE);
        g.setFont(new Font(null, Font.BOLD, 20));
        g.drawString(makeNum(),0,20);
        System.out.println(makeNum());
        // 告诉浏览器，这个请求用图片的方式打开
        resp.setContentType("image/jpeg");
        // 网站存在缓存，不让浏览器缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("Pragma","no-cache");

        // imageio流写数据
        ImageIO.write(image,"jpg",resp.getOutputStream());

    }
		
  	// 随机数
    private String makeNum(){
        Random random = new Random();
        String num = random.nextInt(9999999) + "";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i<7-num.length(); i++){
            sb.append("0");
        }
        num = sb.toString() + num;
        return num;
    }
}

```

#### 11. 重定向和转发

- 相同点

  页面都会实现跳转。

- 不同点

  转发：请求转发的时候，url不会发生变化

  重定向：url会发生变化

#### 

