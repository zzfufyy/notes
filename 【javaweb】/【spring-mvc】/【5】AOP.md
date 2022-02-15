#### AOP

-------

#### 1. 什么是AOP

- 面向切面编程

  Aspect Oriented Programming

  通过预编译方式和运行期动态代理实现程序功能的统一维护。

  利用AOP可以实现对业务逻辑的各个部分进行隔离，

  从而使得各个业务逻辑部分之间的耦合性降低。

  提高了程序的可重用性。

  <img src="imgs/截屏2021-10-10 下午3.10.45.png" alt="截屏2021-10-10 下午3.10.45" style="zoom:67%;" />

- AOP在Spring中的作用

  - 横切关注点：跨越应用程序多个模块的方法或功能
  - 切面：横切关注点被模块化的特殊对象。即，它是一个类。
  - 通知：切面必须完成的工作。即，他是类中的一个方法。
  - 目标：被通知的对象。
  - 代理：向目标对象应用通知之后创建的对象。
  - 切入点：切面通知执行的“地点”。
  - 连接点：与切入点匹配的执行点。

- 在SpringAOP中，通过Advice定义横切逻辑。

  支持5中类型的Advice：

  | 通知类型     | 连接点           | 实现接口                                        |
  | ------------ | ---------------- | ----------------------------------------------- |
  | 前置通知     | 方法前           | org.springframework.aop.MethodBeforeAdvice      |
  | 后置通知     | 方法后           | org.springframework.aop.AfterReturningAdvice    |
  | 环绕通知     | 方法前后         | org.aopalliance.intercept.MethodInterceptor     |
  | 异常抛出通知 | 方法抛出异常     | org.springframework.aop.ThrowsAdvice            |
  | 引介通知     | 类中增加新的方法 | org.springframework.aop.IntroductionInterceptor |

  AOP在不改变原有代码的情况下，去增加新的功能

#### 2. 使用Spring的API接口实现AOP

- 导入包

  ```xml
  <dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.1</version>
  </dependency>
  ```

- 接口

  ```java
  package com.kuang.service;
  
  public interface UserService {
      public void add();
      public void delete();
      public void update();
      public void select();
  }
  
  ```

- 实现类

  ```java
  package com.kuang.service;
  
  public class UserServiceImpl implements UserService{
      @Override
      public void add() {
          System.out.println("增加");
      }
  
      @Override
      public void delete() {
          System.out.println("删除");
      }
  
      @Override
      public void update() {
          System.out.println("更新");
      }
  
      @Override
      public void select() {
          System.out.println("查询");
      }
  }
  
  ```

- LOG

  ```java
  package com.kuang.log;
  
  import org.springframework.aop.MethodBeforeAdvice;
  
  import java.lang.reflect.Method;
  
  public class Log implements MethodBeforeAdvice {
  
      @Override
      public void before(Method method, Object[] objects, Object o) throws Throwable {
          System.out.println(o.getClass().getName() + "的" + method.getName() + "被执行了");
      }
  }
  //////////////////////
  
  package com.kuang.log;
  
  import org.springframework.aop.AfterReturningAdvice;
  
  import java.lang.reflect.Method;
  
  public class AfterLog implements AfterReturningAdvice {
  
      // returnValue： 返回值
      @Override
      public void afterReturning(Object resultValue, Method method, Object[] objects, Object o1) throws Throwable {
          System.out.println("执行了" +method.getName() + ",返回结果为" + resultValue);
      }
  }
  
  ```

- 配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          https://www.springframework.org/schema/aop/spring-aop.xsd">
  
      <!-- 注册bean    -->
      <bean id="userService" class="com.kuang.service.UserServiceImpl"></bean>
      <bean id="log" class="com.kuang.log.Log"></bean>
      <bean id="afterLog" class="com.kuang.log.AfterLog"></bean>
  
      <!-- 配置aop    -->
      <aop:config>
          <!--  切入点    expression:表单时   execution(要执行的位置! 修饰词 返回值 类名 方法名 参数)  -->
          <aop:pointcut id="pointcut1" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
  
          <!--  执行环绕增加      -->
          <aop:advisor advice-ref="log" pointcut-ref="pointcut1"/>
          <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut1"/>
      </aop:config>
  
  </beans>
  ```

- 测试

  ```java
  import com.kuang.service.UserService;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  public class MyTest {
      public static void main(String[] args) {
          ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
          UserService userService =  (UserService) context.getBean("userService");
          userService.add();
  
      }
  }
  ```

#### 3. 使用自定义类实现AOP

- 自定义类

  ```java
  package com.kuang.diy;
  
  public class DiyPointCut {
      public void before(){
          System.out.println("方法执行前");
      }
      public void after(){
          System.out.println("方法执行后");
      }
  }
  
  ```

- 配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          https://www.springframework.org/schema/aop/spring-aop.xsd">
  
      <!-- 注册bean    -->
      <bean id="userService" class="com.kuang.service.UserServiceImpl"></bean>
      <bean id="log" class="com.kuang.log.Log"></bean>
      <bean id="afterLog" class="com.kuang.log.AfterLog"></bean>
  
      <bean id="diy" class="com.kuang.diy.DiyPointCut"/>
  
      <aop:config>
          <aop:aspect ref="diy">
              <!--    切入点        -->
              <aop:pointcut id="point" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
              <!--    通知        -->
              <aop:before method="before" pointcut-ref="point"/>
              <aop:after method="after" pointcut-ref="point"/>
          </aop:aspect>
      </aop:config>
  </beans>
  ```

- 测试

  ```java
  import com.kuang.service.UserService;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  public class MyTest {
      public static void main(String[] args) {
          ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
          UserService userService =  (UserService) context.getBean("userService");
          userService.add();
  
      }
  }
  ```

#### 4. 注解实现AOP

- 自定注解类

  ```java
  package com.kuang.diy;
  
  import org.aspectj.lang.ProceedingJoinPoint;
  import org.aspectj.lang.Signature;
  import org.aspectj.lang.annotation.After;
  import org.aspectj.lang.annotation.Around;
  import org.aspectj.lang.annotation.Aspect;
  import org.aspectj.lang.annotation.Before;
  
  @Aspect
  public class AnnotationPointCut {
      @Before("execution(* com.kuang.service.UserServiceImpl.*(..))")
      public void before(){
          System.out.println("方法执行前");
      }
  
      @After("execution(* com.kuang.service.UserServiceImpl.*(..))")
      public void After(){
          System.out.println("方法执行后");
      }
  
      @Around("execution(* com.kuang.service.UserServiceImpl.*(..))")
      public void around(ProceedingJoinPoint jp) throws Throwable {
          System.out.println("环绕前");
          Signature signature = jp.getSignature();
          System.out.println("signature:" + signature);
          Object proceed = jp.proceed();
          System.out.println("环绕后");
      }
  
  }
  
  ```

- 配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          https://www.springframework.org/schema/aop/spring-aop.xsd">
  
      <!-- 注册bean    -->
      <bean id="userService" class="com.kuang.service.UserServiceImpl"></bean>
      <bean id="log" class="com.kuang.log.Log"></bean>
      <bean id="afterLog" class="com.kuang.log.AfterLog"></bean>
  
      <bean id="annotationPointCut" class="com.kuang.diy.AnnotationPointCut"/>
      <!--  开启注解支持   -->
      <aop:aspectj-autoproxy/>
  
  </beans>
  ```

- 测试

  ```java
  import com.kuang.service.UserService;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  public class MyTest {
      public static void main(String[] args) {
          ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
          UserService userService =  (UserService) context.getBean("userService");
          userService.add();
      }
  }
  ```