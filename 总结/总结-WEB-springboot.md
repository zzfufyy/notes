### 总结-WEB-springboot

--------

#### 1. Spring boot

- 什么是Spring boot

  开源框架，开箱即用。
  
  约定大于配置的开发框架。
  
- starter

  starter启动器整合依赖。

  父依赖：

  ```xml
  <parent>
  	<artifactId>spring-boot-starter-parent</artifactId>
  </parent>
  <!-- 其中父依赖 -->
  <parent>
  	<artifactId>spring-boot-dependencies</artifactId>
  </parent>
  
  <dependencies>
  	<dependecy>
    	<artifactId>spring-boot-starter-web</artifactId>
    </dependecy>
  </dependencies>
  ```

  springboot自己整合的jar包

  如：spring-boot-starter-tomcat

- 配置绑定

  ```java
  @Component
  @ConfigurationProperties(prefix = "person")
  public class Person {
      private String lastName;
  }
  
  @Component
  public class Person {
      @Value("${person.lastName}")
      private String lastName;
      @Value("${person.age}")
  }
  
  @PropertySource(value = "classpath:person.properties")//指向对应的配置文件
  @Component
  @ConfigurationProperties(prefix = "person")
  public class Person {
      private String lastName;
      private Integer age;
  }
  ```

- 自动配置原理

  扫描 所有jar包 META-INF/spring.factories文件

  其中

  ```properties
  # Auto Configure
  org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
  org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
  org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
  org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration,\
  org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration,\
  org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguratio,\...
  ```

  即 接口限定名  =  实现类限定名 x N

  由`org.springframework.core.io.support.SpringFactoriesLoader`

  ```java
  private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader)
  // 加载所有 spring.factories文件内容，并以map形式返回
  ```

- 自动配置原理2

  spring boot入口类：

  ```java
  package com.kuang;
  
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  
  @SpringBootApplication
  public class SpringbootWebappApplication {
      public static void main(String[] args) {
          SpringApplication.run(SpringbootWebappApplication.class, args);
      }
  }
  ```

  注解 **@SpringBootAplication** 中：

  - @SpringBootConfiguration

  - **@EnableAutoConfiguration**

    - @AutoConfigurationPackage

    - **@Import({AutoConfigurationImportSelector.class})**

      AutoConfigurationImportSelector类。

      - getImportGroup() 方法  获取**return** AutoConfigurationImportSelector.AutoConfigurationGroup.**class**;

      - Process() 方法   获取spring.factories配置类的集合。 使用了SpringFactoriesLoader.loadFactoreis方法

      - selectImports() 方法   得到自动配置类，过滤、排除后添加到容器中  

        ```properties
        # Auto Configure
        org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
        org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
        org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
        ```

        其中很多在各种xxxAutoConfiguration中，

        派生条件注解

        @ConditionalOnClass

        @ConditionalOnProperty

        @ConditionalOnResource 

        等。  为过滤条件，只有指定条件满足时，才会加入。

        如这种，

        ```java
        @EnableConfigurationProperties({MongoProperties.class})
        ```

        可以查看配置文件。

- 定制Springmvc

  ```java
  //实现 WebMvcConfigurer 接口可以来扩展 SpringMVC 的功能
  //@EnableWebMvc   不要接管SpringMVC
  @Configuration
  public class MyMvcConfig implements WebMvcConfigurer {
      @Override
      public void addViewControllers(ViewControllerRegistry registry) {
          //当访问 “/” 或 “/index.html” 时，都直接跳转到登陆页面
          registry.addViewController("/").setViewName("login");
          registry.addViewController("/index.html").setViewName("login");
      }
  }
  
  // 完全接管
  //实现 WebMvcConfigurer 接口可以来扩展 SpringMVC 的功能
  @EnableWebMvc  // 完全接管SpringMVC
  @Configuration
  public class MyMvcConfig implements WebMvcConfigurer {
      @Override
      public void addViewControllers(ViewControllerRegistry registry) {
          //当访问 “/” 或 “/index.html” 时，都直接跳转到登陆页面
          registry.addViewController("/").setViewName("login");
          registry.addViewController("/index.html").setViewName("login");
      }
  }
  ```

  

  

​	



