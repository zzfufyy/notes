### JavaBean

#### 1. 概念

- 实体类

- 特定规范写法：

  - 必须有一个无参构造函数
  - 属性必须私有化
  - 必须有对应的get/set方法

- 用处：

  一般用来和数据库字段做映射，即ORM

- ORM概念 Object-Relational Mapping

  - 表 -- 类
  - 字段 -- 属性
  - 行记录 -- 对象

#### 2. 实践1 -- 与 JSP

```jsp
<%@page import="com.kuang.pojo.People"%>
<jsp:userBean id="people" class="com.kuang.pojo.People" scope="page"/>

<jsp:setProperty name="people" property="id" value="23"/>

ID是：<jsp:getProperty name="people" property="id"/>

```



