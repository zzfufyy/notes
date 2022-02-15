### 总结-WEB-JSP

-----

#### 1. jsp基础

- 是什么

  java服务器页面，本质也是servlet。

- 生命周期

  jspInit();

  _jspService();

  jspDestroy();

- 语法

  核心

  <% out.println("haha")%>

  代表 <jsp:scriptlet jsp:scriptlet>

  ```jsp
  指令
  <%@ %>
  声明
  <%! int i=0; %>
  表达式
  <%= (new java.util.Date().toLocalString())%>
  ```

  - 指令

    @ page        定义页面属性

    @ include

    @ taglib       引入标签库

  - 内置对象

    request  response  session application  config

    page pagecontext

    out exception

  - 动作

    Jsp:include 

    jsp:usebean

    Jsp:setProperty

    jsp:forward

    

​			
