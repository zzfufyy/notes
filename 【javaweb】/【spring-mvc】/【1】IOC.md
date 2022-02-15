### IOC

------

#### 1. IOC理论推导

- 不用IOC的实现方法

  - 使用dao
  - 不断添加Impl类，用户实际调用的是Impl类。
  - 利用set实现动态实现值的注入（使程序失去主动性，接收对象）

  在之前的业务中，用户的需求可能会影响我们原来的代码。

  我们需要根据用户的需求去修改原代码。

  修改原代码代价高。

- IOC本质

  **控制反转是一种通过描述（XML或注解），并通过第三方去产生或获取特定对象的方式**

  **对象由Spring去控制、管理及装配。**

  Spring中实现的是IOC容器，其实现方法是**依赖注入**，DI.

  **DI是实现IOC的一种方式**

  spring的核心内容。

  使用多种方式完美的实现了IOC，可以使用XML配置，也可以使用注解。

  新版本的spring可以零配置实现IOC

  **spring容器在初始化时先读取配置文件**

  **根据配置文件或元数据创建与组织对象存入容器中。**

  程序使用时再从ioc容器中取出需要的对象。

  <img src="imgs/截屏2021-08-19 下午9.11.03.png" alt="截屏2021-08-19 下午9.11.03" style="zoom:50%;" />
  
  采用XML方式配置Bean的时候，Bean的定义信息和实现分离的。
  
  而采用注解的方式可以把二者合为一体。

------------

#### 2. HelloSpring

- hello

  ```java
  package com.kuang.pojo;
  
  public class Hello {
      private String str;
  
      public String getStr() {
          return str;
      }
  
      public void setStr(String str) {
          this.str = str;
      }
  
      @Override
      public String toString() {
          return "Hello{" +
                  "str='" + str + '\'' +
                  '}';
      }
  }
  ```

- applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd">
  
          <bean id="hello" class="com.kuang.pojo.Hello">
              <property name="str" value="Spring"></property>
          </bean>
  </beans>
  ```

- Test

  ```java
  import javafx.application.Application;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  import com.kuang.pojo.Hello;
  public class MyTest {
      public MyTest() {
      }
  
      public static void main(String[] args) {
          // 获取spring的上下文对象
          ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
          // 我们的对象现在都在spring中管理了
          // 对象取出来即可
          Hello hello = (Hello)context.getBean("hello");
          System.out.println(hello.toString());
      }
  }
  ```

- 引用不同接口的数据驱动

  - appllicationContext.xml

    ```xml
    <bean id="UserServiceImpl" class="com.kuang.service.UserServiceImpl">
    	<!-- 实际付给 变量引用-->
      <property name="userDao"  ref="oracleImpl"></property>
    </bean>
    ```

  - 测试

    ```java
    ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserServiceImpl usi = (UserServiceImpl)context.getBean("UserServiceImpl");
    usi.getUser();  // 获取到了oracleImpl 实现类的实例
    ```



#### 3. IOC创建对象的方式

- 无参构造创建对象

- 有参构造创建对象

  ```xml
  <bean id="user" class="com.kuang.pojo.User">
  	<constructor-arg index="0" value="750000"/>
  </bean>
  
  <bean id="user" class="com.kuang.pojo.User">
  	<constructor-arg type="java.lang.String" value="zyw"/>
  </bean>
  
  <!-- 直接通过参数名  推荐 -->
  <bean id="user" class="com.kuang.pojo.User">
  	<constructor-arg name="name" value="zyw"/>
  </bean>
  ```

  