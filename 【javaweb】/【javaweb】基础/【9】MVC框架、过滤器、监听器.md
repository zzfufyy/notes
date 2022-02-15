### MVC框架、过滤器、监听器

------------

#### 1. 概念

- 什么是MVC

  Model - Veiw - Controller

  - Model

    1. 业务处理：业务逻辑 -- Service

    2. 数据库持久层(CRUD) -- DAO

  - View - JSP

    1. 展示数据
    2. 提供连接发起Servlet请求(a， form， img...)

  - Controller - Servlet

    1. 接收用户请求 （req：请求参数、session信息...）
    2. 交给业务层去做响应内容
    3. 重定向或者转发，控制视图跳转

#### 2. 过滤器 -- Filter

- 作用

  - 处理中文乱码
  - 登录验证...

- 实例

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                                http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
      <servlet>
          <servlet-name>show</servlet-name>
          <servlet-class>com.zyw.servlet.ShowServlet</servlet-class>
      </servlet>
      <servlet-mapping>
          <servlet-name>show</servlet-name>
          <url-pattern>/show</url-pattern>
      </servlet-mapping>
  
      <filter>
          <filter-name>CharacterEncodingFilter</filter-name>
          <filter-class>com.zyw.filter.CharacterEncodingFilter</filter-class>
      </filter>
      <filter-mapping>
          <filter-name>CharacterEncodingFilter</filter-name>
          <!--  /* 就是所有请求      -->
          <url-pattern>/show</url-pattern>
      </filter-mapping>
  </web-app>
  ```

  ```java
  // ShowServlet
  package com.zyw.servlet;
  
  import javax.servlet.ServletException;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  public class ShowServlet extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  
          // 如果没有过滤器或者   set utf-8 这是乱码
          resp.getWriter().write("你好呀，世界！");
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          super.doPost(req, resp);
      }
  }
  
  ```

  ```java
  // CharacterEncodingFilter
  package com.zyw.filter;
  
  
  import javax.servlet.*;
  import java.io.IOException;
  
  public class CharacterEncodingFilter implements Filter {
  
      // 初始化
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
          System.out.println("CharacterEncodingFilter启动");
      }
  
      /*
      1. 过滤中的所有代码，在过滤特定请求的时候会执行
      2. 必须要让过滤器继续通行
      * */
  
      @Override
      public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
          servletResponse.setCharacterEncoding("utf-8");
          servletRequest.setCharacterEncoding("utf-8");
          servletResponse.setContentType("text/html;charset=UTF-8");
  
          System.out.println("CharacterEncodingFilter执行前....");
          filterChain.doFilter(servletRequest,servletResponse); // 让我们的请求继续走，如果不写程序到这里就停止了
          System.out.println("CharacterEncodingFilter执行后....");
      }
  
      // web服务器关闭的时候，销毁
      @Override
      public void destroy() {
          System.out.println("CharacterEncodingFilter销毁");
      }
  }
  
  ```

#### 3. 监听器

- 概念

  监听事件。

- 实例

  ```xml
  <!-- web.xml -->
  <listener>
    <listener-class>com.zyw.listener.OnlineCountListener</listener-class>
  </listener>
  ```

  ```java
  package com.zyw.listener;
  
  import javax.servlet.ServletContext;
  import javax.servlet.http.HttpSessionEvent;
  import javax.servlet.http.HttpSessionListener;
  
  // 实现session监听方法
  public class OnlineCountListener implements HttpSessionListener {
      // 创建session监听
      @Override
      public void sessionCreated(HttpSessionEvent se) {
          ServletContext ctx = se.getSession().getServletContext();
          Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
          if (onlineCount == null){
              onlineCount = new Integer(1);
          }else{
              int count = onlineCount.intValue();
              onlineCount = new Integer(count+1);
          }
          ctx.setAttribute("OnlineCount", onlineCount);
  
      }
  
      // 一旦销毁session就会触发一次这个事件
      @Override
      public void sessionDestroyed(HttpSessionEvent se) {
          ServletContext ctx = se.getSession().getServletContext();
          Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
          if (onlineCount == null){
              onlineCount = new Integer(1);
          }else{
              int count = onlineCount.intValue();
              onlineCount = new Integer(count-1);
          }
          ctx.setAttribute("OnlineCount", onlineCount);
  
      }
  }
  
  ```

  

  ```jsp
  <!-- jsp -->
  <%@ page contentType="text/html;charset=UTF-8" language="java"%>
  
  <html>
  <body>
  <h2>Hello World!</h2>
  <h1>当前有<span><%=this.getServletConfig().getServletContext().getAttribute("OnlineCount")%> </span> 人在线</h1>
  </body>
  </html>
  
  ```

  

