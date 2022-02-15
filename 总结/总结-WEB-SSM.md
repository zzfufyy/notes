JAVA_WEB SSM

-------

#### 1. Servlet

- 什么是Servlet

  针对动态页面的一套开发规范。

  servlet程序  在 servlet容器中运行。

  Servlet接口   GenericServlet抽象类  HttpServlet

  方法： init  service destroy

- HttpServlet

  1. http协议的请求方法：

     ```java
     GET  POST
     HEAD PUT 
     DELETE TRACE
     OPTIONS
     ```

  2. 对象

     HttpServletRequest

     HttpServletResponse

     ServletContext

- 转发与重定向

  转发是服务端行为，url不改变。

  重定向是客户端行为，url改变。

  得到RequestDispatcher对象。

  ServletContext.getRequestDispatcher(path).forward(req, resp);

  ServletRequest.getRequestDispatcher(path);

​		ServletResponse.sendRedirect("/doNext");

---------------

#### 2. Spring

- Spring是什么

  以AOP和IOC为核心的开发框架。

  基于Bean的编程框架。

- 体系结构

  - DAO

    jdbc orm transactions oxm jms 

  - WEB

    servlet web websocket portlet

  - UTILS

    aop aspects util message

  - CORE

    beans core context spel

- IOC容器

  类的实例化交由容器管理。

  BeanFactory

  ApplicationContext

- DI 依赖注入

  - 构造器注入

  - setter注入

  - 自动装配

    autowire="byName"  "byType"

  - 注解装配

    ```xml
    <context:component-scan base-package="com.zyw"/>
    ```

    @Component

    @Controller

    @Service

    @Repository

    @Autowired 类型匹配   @Qualifier

    @Resource  id名称匹配

- AOP

  - 原理：

    BeanPostprocessor   后置处理器

    切面：  切入点   增强advice   

    目标： 连接点

    切面动态代理目标。

  - 示例

    ```xml
    <aop:config>
    	<aop:aspect id="log" ref="logging">
      	<aop:pointcut id="selectAll" expression="execution(* org.zyw.*.*(..))"/>
        <aop:before point-ref="selectAll" method="beforeAdvice"/>
      </aop:aspect>
    </aop:config>
    ```

- 事务管理

  - ACID原则

    A：Atomic 原子性

    C: consistency  一致性

    I：Isolation 隔离性

    D: Durablity  持久性

-------

#### 3. Springmvc

- 什么是springmvc

  基于mvc设计模式的spring开发框架

  核心是   DispatcherServlet

- DispatcherServlet

  前端控制器：

  视图解析器   viewResolver   

  HandlerMapping

  HanderAdapter

  ```xml
  
  <context:component-scan base-package="com.kuang.controller"/>
  <mvc:default-servlet-handler/>
  <mvc:annotation-driven/>
   <bean id="InternalResourceViewResolver"
         class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <property name="prefix" value="/WEB-INF/jsp/"/>
          <property name="suffix" value=".jsp"/>
      </bean>
  ```

-------

#### 4. Mybatis

- 什么是Mybatis

  半自动持久层框架。在实体类和SQL语句之间建立映射关系，ORM。

- 与Hibernate区别

  Mybatis是半自动框架，维护的是POJO和SQL的映射关系。

  ​		每个映射需要自定义缓存配置。

  Hibernate 是全表映射框架，对应POJO和表的映射关系，不需要编写大量sql。

  ​		对查询对象的缓存有良好的管理机制。

  Mybatis更加灵活，Hibernate适合业务更加稳定的项目。

- 核心对象

  SqlSessionFactory 生产sqlSession对象。

  **SqlSession**，类似于Connection对象。

  作用域在与request的作用域或者方法体。

- 缓存

  1级： hashmap本地缓存，缓存sql语句，session范围内。

  2级： 全局缓存。缓存结果对象，被所有sqlsession共享。

  一般用memcached左缓存。

​		

