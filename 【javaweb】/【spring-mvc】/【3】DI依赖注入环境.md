### DI依赖注入环境

------------------

- 依赖注入理解

  - 依赖：

    **bean对象的创建依赖于容器**

  - 注入：

    **bean对象的所有属性，由容器来注入**

#### 1. 构造器注入

- IOC中已举例。

- 举例

  ```xml
  
  <bean id="user" class="com.kuang.pojo.User">
  	<constructor-arg name="name" value="zyw"/>
  </bean>
  ```

#### 2. SET方式注入

- 举例

  ```xml
  <bean id="hello" class="com.kuang.pojo.Hello">
      <property name="name" value="zyw"/>
    	<property name="address" ref="address"/>
  	  <property name="books">
    		<array>
          <value>anbcd</value>
          <value>asdasd</value>
          <value>asdasda</value>
        </array>  
  	  </property>
    	<property name="card">
        <map>
        	<entry key="身份证" value="asdahsdkjahskjd"></entry>
        </map>
  	  </property>
    
    	
  </bean>
  ```

  

#### 3. 其他方式注入

- 增加命名空间

  - p命名

    `xmlns:p="http://www.springframework.org/schema/p"`

  - c命名

    `xmlns:c="http://www.springframework.org/schema/c"`

- p命名标签使用

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd">
          <!--   直接注入属性值      <-->
          <bean id="user" class="com.kuang.pojo.Student" p:name="zyw" ></bean>
  
  
  </beans>
  ```
  
- c命名标签使用

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xmlns:c="http://www.springframework.org/schema/c"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd">
  
          <bean id="hello" class="com.kuang.pojo.Hello">
              <property name="str" value="Spring"></property>
          </bean>
  
          <!--   直接注入属性值   property   <-->
          <bean id="user" class="com.kuang.pojo.Student" p:name="zyw" ></bean>
  
          <!--   通过构造器注入  contstruct-args     -->
          <bean id="user" class="com.kuang.pojo.Student" c:name="zyw"></bean>
  
  </beans>
  ```

#### 4. bean的作用域

- 单例模式（Spring默认机制）

  2个 getbean出来的对象是同一个对象，不会创建新的。

  ```xml
  <bean id="user2" class="com.kuang.pojo.User" c:age="18" c:name="zyw"
        scope="singleton"/>
  ```

- 原型模式

  每次从容器中get的时候，都会产生一个新的对象。

- request、session、application、websocket这些只能在web开发中使用

#### 5. bean的自动装配

- 自动装配

  - spring满足bean依赖的一种方式
  - spring会在上下文自动寻找，并自动给bean装配属性
  - 三种装配方式：
    1. xml中显式配置
    2. java中显式配置
    3. **隐式配置**

- 实例

  ```xml
  <bean id="cat" class="com.kuang.pojo.Cat"/>
  <bean id="dog" class="com.kuang.pojo.Dog"/>
  <bean id="People" class="com.kuang.pojo.People" autowire="byName">
    <property name="name" value="zyw"/>
  </bean>
  ```

  - byName

    会在容器上下文中查找，和set对应的beanid

  - byType

    会在容器中查找，和自己对象属性类型相同的bean

#### 6. 使用注解实现自动装配

​	jdk1.5实现，spring2.5实现。

- 使用前须知

  - 导入约束

  - 配置注解的支持

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            https://www.springframework.org/schema/context/spring-context.xsd">
    
        <context:annotation-config/>
    
    </beans>
    ```

- Autowired注解

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd">
    
    	<context:annotation-config/>
  		<bean id="cat" class="com.kuang.pojo.Cat"/>
  		<bean id="dog" class="com.kuang.pojo.Dog"/>
  		<bean id="People" class="com.kuang.pojo.People"/>
  </beans>
  ```

  ```java
  public class People{
    // 可以忽略set方法
    @Autowired
    private Cat cat;
    @Autowired
    private Dog dog;
  }
  ```

  - @Autowired(required = false)，表示这个对象可以为null
  - @Nullable 标记了这个字段，表示这个字段可以为null
  - @Qualifier(value="cat1111")（多个class相同id找不到的情况下，指定id值）
  - @Resource(name="cat1111")  和Qualifier作用差不多

- Autowired 和 Resource注解的区别

  - 自动装配，都可以放在属性字段上
  - Autowired使用byType实现，必须要求有这个对象
  - **Resource默认使用byName实现，如果找不到，则通过byType实现。**

  - 执行顺序：

    - autowired通过类型、名字(id)

      如果autowired不能唯一，则需要通过Quilifier(value="")

    - Resource 通过名字、类型

#### 7. 使用注解开发

- 前置

  Spring4之后，使用注解开发必须导入aop的包。

  xml中导入context约束，支持。

- 实例

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd">
  
      <!-- 指定要扫描的包，这个包下的注解就会生效    -->
      <context:component-scan base-package="com.kuang.pojo"/>
      <context:annotation-config/>
      
  </beans>
  ```

  ```java
  @Component
  public class User{
    @Value("zyw")
    public String name;
    
    @Value("zyw")
    public void setName(String name){
      this.name=name;
    }
  }
  ```

- 衍生注解

  Component有几个衍生注解，按照mvc三层架构分层

  - dao @Repository
  - service @Service
  - Controller @Controller

  这4个注解功能都是一样的，都是代表将某个类注册到Spring容器中，装配Bean。

- @Scope

  @Scope("singleton")

  @Scope("prototype")

- 小结

  xml与注解：

  - xml更加万能
  - 注解不是自己类使用不了，维护相对复杂。

  最佳实践：

  - xml用来管理bean
  - 注解只负责管理属性的注入。
  - 我们在使用的过程中，只需要注意一个问题：必须要让注解生效，就需要开解注解支持

#### 8. 使用Javaconfig配置Spring

- 目的

  完全不使用Spring的xml配置，完全交给java来做

  JavaConfig以前是Spring的一个子项目，在Spring4之后，变成了一个核心功能。

- 实例

  ```java
  package com.kuang.config;
  
  import com.kuang.pojo.User;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.annotation.AnnotationConfigApplicationContext;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  @Configuration
  public class KuangConfig {
  		
    	// 注册一个bean，相当于一个bean标签
    	// 方法的名字相当于id属性
      // 返回值，相当于class属性
      @Bean
      public User getUser(){
          return new User(); // 注入bean的对象
      }
  
      public static void main(String[] args) {
          ApplicationContext appContext = new AnnotationConfigApplicationContext(KuangConfig.class);
          User user = (User)appContext.getBean("getUser");
          System.out.println(user.toString());
      }
  }
  
  ```

  这种纯java配置的方式，在springboot中随处可见。