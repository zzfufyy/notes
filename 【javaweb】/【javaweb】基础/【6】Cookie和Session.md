### Cookie和Session

-----------------------

#### 1. Session 会话

- 会话

  用户打开一个浏览器，各种操作，知道关闭浏览器。这个过程就是一次会话。

- 有状态会话（保存了cookie等）

  一个网站怎么证明你来过？

  客户端    服务端

  1. 服务端给客户端一个信件，客户端下次访问服务端带上信件就可以了。

     这就是cookie。

  2. 服务器等级你来过了，下次你来的时候我来匹配你。

#### 2. 保存会话的两种技术

- cookie
  - 客户端技术（响应、请求）
- session
  - 服务器技术（利用这个技术可以保存用户的会话信息，把信息放在session中）

#### 3. cookie

-  从请求中拿到cookie信息
- 服务器端响应给客户端cookie
- cooke一般会保存在本地的用户目录appdata

- 细节：
  - 一个cookie只能保存一个信息
  - 一个web可以给浏览器发送多个cookie，最多20个
  - cookie大小有限制 4kb
  - 300个cookie浏览器上线
- 删除cookie
  - 不设置有效期，关闭浏览器，自动失效。
  - 设置有效期为0；

一些方法：

```)*java
Cookie[] cookies = req.getCookies();
cookie.getName();
cookie.getValue();
new Cookie("lastLoginTime", System.currentTimeMillis() + "");
cookie.setMaxAge(24*60*60);
resp.addCookie(cookie);
```



```java
package com.zyw.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

// 保存用户上一次访问的时间
public class CookieServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        PrintWriter out = resp.getWriter();

        // Cookie 服务端从客户端获取：
        Cookie[] cookies = req.getCookies();

        // 判断Cookie是否存在
        if(cookies!=null){
            out.write("你上一次访问的时间是:");
            for(int i = 0; i<cookies.length; i++){
                Cookie cookie = cookies[i];
                if(cookie.getName().equals("lastLoginTime")){
                    long lastLoginTime = Long.parseLong(cookie.getValue());
                    Date date = new Date(lastLoginTime);
                    out.write(date.toLocaleString());
                }
            }
        }else{
            out.write("这是您第一次访问本站");
        }

        // 服务给客户端响应一个cookie：
        Cookie cookie = new Cookie("lastLoginTime",System.currentTimeMillis() + "");

        // 保存一天
        cookie.setMaxAge(24*60*60);
        resp.addCookie(cookie);
    }
}

```

<img src="imgs/截屏2021-07-05 下午11.13.34.png" style="zoom:80%;" />

#### 4. Session

1. 服务器会给每个用户（浏览器）创建一个session对象
2. 一个session独占一个浏览器，只要浏览器没有关闭，这个session就一直存在
3. 保存各种信息

```java
package com.zyw.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;

public class SessionServlet extends HttpServlet {
    // 解决乱码问题

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text.html;charset=utf-8");

        // 得到Session
        HttpSession session = req.getSession();
        session.setAttribute("name","zyw");
        String sessionId = session.getId();
        if(session.isNew()){
            resp.getWriter().write("session创建成功:"+sessionId);

        }else{
            resp.getWriter().write("session已经在服务器中存在了："+ sessionId);
        }
    }


}
```

#### 5.cookie和session的区别

- cookie是把用户的数据写给用户的浏览器，浏览器保存
- session是把用户的数据写到用户独占的session中，服务器端保存
- session对象由服务创建。

- 使用场景：
  - 保存一个登录用户的信息
  - 购物车信息
  - 在整个网站中经常会使用的数据，我们将它保存在session中。