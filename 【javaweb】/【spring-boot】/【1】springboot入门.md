### springboot入门

-------

#### 1. Springboot程序

- 基本项目架构

  <img src="imgs/截屏2021-10-29 下午6.46.20.png" alt="截屏2021-10-29 下午6.46.20" style="zoom:50%;" />

- Pom.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.5.6</version>
          <relativePath/> <!-- lookup parent from repository -->
      </parent>
      <groupId>com.kuang</groupId>
      <artifactId>springboottest</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>springboottest</name>
      <description>Demo project for Spring Boot</description>
      <properties>
          <java.version>1.8</java.version>
      </properties>
  
      <dependencies>
          <!--  web依赖： tomcat, dispatcher servlet,xml      -->
          <!--  所有springboot依赖都是  spring-boot-starter开头      -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
  
          <!--  单元测试      -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  
      <build>
          <plugins>
              <plugin>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-maven-plugin</artifactId>
              </plugin>
          </plugins>
      </build>
  
  </project>
  
  ```

- SpringboottestApplication.java

  ```java
  package com.kuang.springboottest;
  
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  
  // 程序的主入口
  @SpringBootApplication
  public class SpringboottestApplication {
  
      public static void main(String[] args) {
          SpringApplication.run(SpringboottestApplication.class, args);
      }
  }
  
  ```

- HelloController.java

  ```java
  package com.kuang.springboottest.controller;
  
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class HelloController {
      @RequestMapping("/hello")
      public String hello(){
          return "hello,world";
      }
  }
  ```

- Application.properties

  

-----------

#### 2. Springboot自动装配原理

- pom.xml

  - 核心依赖是在父管理中。

    ```xml
    <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.5.6</version>
      <relativePath/> <!-- lookup parent from repository -->
    </parent>
    ```

  - 在引入一些依赖不需要写版本，就是因为版本仓库

- 启动器

  ```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
  </dependency>
  ```

  - 启动器说白了就是springboot的启动场景
  - 比如spring-boot-starter-web，他就会帮我们自动导入web环境所需要的依赖
  - springboot会将所有的功能场景，都变成一个个的启动器
  - 如果要使用什么功能，就只需要找到对应的启动器就可以了是

- 注解

  - 结论

    所有的SpringBoot的自动配置

    都是在启动的时候扫描并加载：spring.factories

    但是不一定生效(@ConditionalOnClasss)。

    只要导入了对应的start，就有对应的启动器。

    有了启动器自动装配就会生效。

  - 步骤

    1. springboot启动的时候，从类路径下/META-INF/spring.factories 获取指定的值

    2. 将这些自动配置的类导入容器，自动配置就会生效。

    3. 以前我们需要配置的东西，现在springboot帮我们做了

    4. 整个JavaEE，解决方案和自动配置的东西都在

       **spring-boot-autoconfigure-2.5.6.jar**

    5. 他会把所有需要导入的组件，以类名的方式返回，这些组件就会被添加到容器。

    6. 容器中存在非常多的xxxAutoConfiguration 的文件，就是这些类给容器中导入了这个场景所需要的所有组件。

  - 流程图分析

    ```mermaid
    graph TB
    a[自动配置原理分析]
    b[SpringBootApplication]
    c[&#64SpringBootConfiguration]
    d[&#64EnableAutoConfiguration:自动导入包]
    e[ComponentScan: 扫描当前主启动类同级的包]
    c1[&#64Configuration]
    c11[&#64Component]
    
    d1[&#64AutoConfigurationPackage]
    d2[&#64Import&#40&#123AutoConfigurationImportSelector.class&#41&#125:<br>自动导入包的核心]
    d21[类:AutoConfigurationImportSelector]
    d211[方法:getAutoConfigurationEntry&#40&#41<br>获取自动配置的实体]
    d212[方法:getCandidateConfiguration&#40&#41<br>获取候选的配置]
    d2121[return EnableAutoConfiguration.class]
    d213[loadlFactoryName&#40&#41: 获取所有的加载配置]
    d214[loadSpringFactories&#40&#41]
    d2141[项目资源: <br>classLoader.getResource&#40FACTORIES_RESOURCE_LOCATION&#41]
    d21411[META-INF.spring.factories]
    d2142[系统资源: <br>ClassLoader.getSystemResources&#40FACTORIES_RESOURCE_LOCATION&#41]
    d2143[从这些资源遍历了所有的自动配置后, <br>封装为Properties供我们使用]
    
    a-->b
    b-->c
    c--> c1 -->c11
    b-->d
    
    d-->d1
    d-->d2
    d2-->d21
    d21--> d211
    d21--> d212
    d212-->d2121
    d21--> d213
    d21--> d214
    d214-->d2141-->d21411
    d214-->d2142
    d214-->d2143
    
    
    ```

    

  - 主程序入口

    ```java
    package com.kuang.springboottest;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    // 程序的主入口
    // 标注这个类是一个springboot的应用： 启动类下的所有资源被导入
    @SpringBootApplication
    public class SpringboottestApplication {
        // 启动
        public  static void main(String[] args) {
            SpringApplication.run(SpringboottestApplication.class, args);
        }
    
    }
    ```

    

  - 注解深入

    ```java
    @SpringBootConfiguration：  springboot配置
      @Configuration： spring配置类
    	@Component： 说明这个也是spring的组件
    
    
    @EnableAutoConfiguration： 自动导入配置
      @AutoConfigurationPackage：自动配置包
    	  @Import(AutoConfigurationPackages.Registrar.class)：自动配置"包注册"
      @Import(AutoConfigurationImportSelector.class)： 自动配置导入选择
    
    @ConditionalOnClass(...) 满足条件才会生效
    ```

  - 细节

    - Assert.empty(configurations)

      <img src="imgs/截屏2021-10-29 下午7.17.32.png" alt="截屏2021-10-29 下午7.17.32" style="zoom:80%;" />

    - spring.factories

      ```properties
      # Initializers
      org.springframework.context.ApplicationContextInitializer=\
      org.springframework.boot.autoconfigure.SharedMetadataReaderFactoryContextInitializer,\
      org.springframework.boot.autoconfigure.logging.ConditionEvaluationReportLoggingListener
      
      # Application Listeners
      org.springframework.context.ApplicationListener=\
      org.springframework.boot.autoconfigure.BackgroundPreinitializer
      
      # Environment Post Processors
      org.springframework.boot.env.EnvironmentPostProcessor=\
      org.springframework.boot.autoconfigure.integration.IntegrationPropertiesEnvironmentPostProcessor
      
      # Auto Configuration Import Listeners
      org.springframework.boot.autoconfigure.AutoConfigurationImportListener=\
      org.springframework.boot.autoconfigure.condition.ConditionEvaluationReportAutoConfigurationImportListener
      
      # Auto Configuration Import Filters
      org.springframework.boot.autoconfigure.AutoConfigurationImportFilter=\
      org.springframework.boot.autoconfigure.condition.OnBeanCondition,\
      org.springframework.boot.autoconfigure.condition.OnClassCondition,\
      org.springframework.boot.autoconfigure.condition.OnWebApplicationCondition
      
      # Auto Configure
      org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
      org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
      org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
      org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
      org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration,\
      org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration,\
      org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguration,\
      org.springframework.boot.autoconfigure.context.ConfigurationPropertiesAutoConfiguration,\
      org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration,\
      org.springframework.boot.autoconfigure.context.MessageSourceAutoConfiguration,\
      org.springframework.boot.autoconfigure.context.PropertyPlaceholderAutoConfiguration,\
      org.springframework.boot.autoconfigure.couchbase.CouchbaseAutoConfiguration,\
      org.springframework.boot.autoconfigure.dao.PersistenceExceptionTranslationAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.cassandra.CassandraDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.cassandra.CassandraRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.couchbase.CouchbaseDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.couchbase.CouchbaseRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRestClientAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.jdbc.JdbcRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.jpa.JpaRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.ldap.LdapRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.mongo.MongoDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.mongo.MongoReactiveDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.mongo.MongoReactiveRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.mongo.MongoRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.neo4j.Neo4jDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.neo4j.Neo4jReactiveDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.neo4j.Neo4jReactiveRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.neo4j.Neo4jRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.r2dbc.R2dbcDataAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.r2dbc.R2dbcRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.redis.RedisAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.redis.RedisReactiveAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.redis.RedisRepositoriesAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.rest.RepositoryRestMvcAutoConfiguration,\
      org.springframework.boot.autoconfigure.data.web.SpringDataWebAutoConfiguration,\
      org.springframework.boot.autoconfigure.elasticsearch.ElasticsearchRestClientAutoConfiguration,\
      org.springframework.boot.autoconfigure.flyway.FlywayAutoConfiguration,\
      org.springframework.boot.autoconfigure.freemarker.FreeMarkerAutoConfiguration,\
      org.springframework.boot.autoconfigure.groovy.template.GroovyTemplateAutoConfiguration,\
      org.springframework.boot.autoconfigure.gson.GsonAutoConfiguration,\
      org.springframework.boot.autoconfigure.h2.H2ConsoleAutoConfiguration,\
      org.springframework.boot.autoconfigure.hateoas.HypermediaAutoConfiguration,\
      org.springframework.boot.autoconfigure.hazelcast.HazelcastAutoConfiguration,\
      org.springframework.boot.autoconfigure.hazelcast.HazelcastJpaDependencyAutoConfiguration,\
      org.springframework.boot.autoconfigure.http.HttpMessageConvertersAutoConfiguration,\
      org.springframework.boot.autoconfigure.http.codec.CodecsAutoConfiguration,\
      org.springframework.boot.autoconfigure.influx.InfluxDbAutoConfiguration,\
      org.springframework.boot.autoconfigure.info.ProjectInfoAutoConfiguration,\
      org.springframework.boot.autoconfigure.integration.IntegrationAutoConfiguration,\
      org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration,\
      org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,\
      org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration,\
      org.springframework.boot.autoconfigure.jdbc.JndiDataSourceAutoConfiguration,\
      org.springframework.boot.autoconfigure.jdbc.XADataSourceAutoConfiguration,\
      org.springframework.boot.autoconfigure.jdbc.DataSourceTransactionManagerAutoConfiguration,\
      org.springframework.boot.autoconfigure.jms.JmsAutoConfiguration,\
      org.springframework.boot.autoconfigure.jmx.JmxAutoConfiguration,\
      org.springframework.boot.autoconfigure.jms.JndiConnectionFactoryAutoConfiguration,\
      org.springframework.boot.autoconfigure.jms.activemq.ActiveMQAutoConfiguration,\
      org.springframework.boot.autoconfigure.jms.artemis.ArtemisAutoConfiguration,\
      org.springframework.boot.autoconfigure.jersey.JerseyAutoConfiguration,\
      org.springframework.boot.autoconfigure.jooq.JooqAutoConfiguration,\
      org.springframework.boot.autoconfigure.jsonb.JsonbAutoConfiguration,\
      org.springframework.boot.autoconfigure.kafka.KafkaAutoConfiguration,\
      org.springframework.boot.autoconfigure.availability.ApplicationAvailabilityAutoConfiguration,\
      org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration,\
      org.springframework.boot.autoconfigure.ldap.LdapAutoConfiguration,\
      org.springframework.boot.autoconfigure.liquibase.LiquibaseAutoConfiguration,\
      org.springframework.boot.autoconfigure.mail.MailSenderAutoConfiguration,\
      org.springframework.boot.autoconfigure.mail.MailSenderValidatorAutoConfiguration,\
      org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration,\
      org.springframework.boot.autoconfigure.mongo.MongoAutoConfiguration,\
      org.springframework.boot.autoconfigure.mongo.MongoReactiveAutoConfiguration,\
      org.springframework.boot.autoconfigure.mustache.MustacheAutoConfiguration,\
      org.springframework.boot.autoconfigure.neo4j.Neo4jAutoConfiguration,\
      org.springframework.boot.autoconfigure.netty.NettyAutoConfiguration,\
      org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration,\
      org.springframework.boot.autoconfigure.quartz.QuartzAutoConfiguration,\
      org.springframework.boot.autoconfigure.r2dbc.R2dbcAutoConfiguration,\
      org.springframework.boot.autoconfigure.r2dbc.R2dbcTransactionManagerAutoConfiguration,\
      org.springframework.boot.autoconfigure.rsocket.RSocketMessagingAutoConfiguration,\
      org.springframework.boot.autoconfigure.rsocket.RSocketRequesterAutoConfiguration,\
      org.springframework.boot.autoconfigure.rsocket.RSocketServerAutoConfiguration,\
      org.springframework.boot.autoconfigure.rsocket.RSocketStrategiesAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.servlet.UserDetailsServiceAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.servlet.SecurityFilterAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.reactive.ReactiveSecurityAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.reactive.ReactiveUserDetailsServiceAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.rsocket.RSocketSecurityAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.saml2.Saml2RelyingPartyAutoConfiguration,\
      org.springframework.boot.autoconfigure.sendgrid.SendGridAutoConfiguration,\
      org.springframework.boot.autoconfigure.session.SessionAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.oauth2.client.servlet.OAuth2ClientAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.oauth2.client.reactive.ReactiveOAuth2ClientAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.oauth2.resource.servlet.OAuth2ResourceServerAutoConfiguration,\
      org.springframework.boot.autoconfigure.security.oauth2.resource.reactive.ReactiveOAuth2ResourceServerAutoConfiguration,\
      org.springframework.boot.autoconfigure.solr.SolrAutoConfiguration,\
      org.springframework.boot.autoconfigure.sql.init.SqlInitializationAutoConfiguration,\
      org.springframework.boot.autoconfigure.task.TaskExecutionAutoConfiguration,\
      org.springframework.boot.autoconfigure.task.TaskSchedulingAutoConfiguration,\
      org.springframework.boot.autoconfigure.thymeleaf.ThymeleafAutoConfiguration,\
      org.springframework.boot.autoconfigure.transaction.TransactionAutoConfiguration,\
      org.springframework.boot.autoconfigure.transaction.jta.JtaAutoConfiguration,\
      org.springframework.boot.autoconfigure.validation.ValidationAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.client.RestTemplateAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.embedded.EmbeddedWebServerFactoryCustomizerAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.HttpHandlerAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.ReactiveWebServerFactoryAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.WebFluxAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.error.ErrorWebFluxAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.function.client.ClientHttpConnectorAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.reactive.function.client.WebClientAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.DispatcherServletAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.ServletWebServerFactoryAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.HttpEncodingAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.MultipartAutoConfiguration,\
      org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration,\
      org.springframework.boot.autoconfigure.websocket.reactive.WebSocketReactiveAutoConfiguration,\
      org.springframework.boot.autoconfigure.websocket.servlet.WebSocketServletAutoConfiguration,\
      org.springframework.boot.autoconfigure.websocket.servlet.WebSocketMessagingAutoConfiguration,\
      org.springframework.boot.autoconfigure.webservices.WebServicesAutoConfiguration,\
      org.springframework.boot.autoconfigure.webservices.client.WebServiceTemplateAutoConfiguration
      
      # Failure analyzers
      org.springframework.boot.diagnostics.FailureAnalyzer=\
      org.springframework.boot.autoconfigure.data.redis.RedisUrlSyntaxFailureAnalyzer,\
      org.springframework.boot.autoconfigure.diagnostics.analyzer.NoSuchBeanDefinitionFailureAnalyzer,\
      org.springframework.boot.autoconfigure.flyway.FlywayMigrationScriptMissingFailureAnalyzer,\
      org.springframework.boot.autoconfigure.jdbc.DataSourceBeanCreationFailureAnalyzer,\
      org.springframework.boot.autoconfigure.jdbc.HikariDriverConfigurationFailureAnalyzer,\
      org.springframework.boot.autoconfigure.jooq.NoDslContextBeanFailureAnalyzer,\
      org.springframework.boot.autoconfigure.r2dbc.ConnectionFactoryBeanCreationFailureAnalyzer,\
      org.springframework.boot.autoconfigure.session.NonUniqueSessionRepositoryFailureAnalyzer
      
      # Template availability providers
      org.springframework.boot.autoconfigure.template.TemplateAvailabilityProvider=\
      org.springframework.boot.autoconfigure.freemarker.FreeMarkerTemplateAvailabilityProvider,\
      org.springframework.boot.autoconfigure.mustache.MustacheTemplateAvailabilityProvider,\
      org.springframework.boot.autoconfigure.groovy.template.GroovyTemplateAvailabilityProvider,\
      org.springframework.boot.autoconfigure.thymeleaf.ThymeleafTemplateAvailabilityProvider,\
      org.springframework.boot.autoconfigure.web.servlet.JspTemplateAvailabilityProvider
      
      # DataSource initializer detectors
      org.springframework.boot.sql.init.dependency.DatabaseInitializerDetector=\
      org.springframework.boot.autoconfigure.flyway.FlywayMigrationInitializerDatabaseInitializerDetector
      
      # Depends on database initialization detectors
      org.springframework.boot.sql.init.dependency.DependsOnDatabaseInitializationDetector=\
      org.springframework.boot.autoconfigure.batch.JobRepositoryDependsOnDatabaseInitializationDetector,\
      org.springframework.boot.autoconfigure.quartz.SchedulerDependsOnDatabaseInitializationDetector,\
      org.springframework.boot.autoconfigure.session.JdbcIndexedSessionRepositoryDependsOnDatabaseInitializationDetector
      ```

    --------

    #### 3. 原理探讨

    - SpringApplication

      这个类主要做了以下四件事：

      1. 推断应用是普通项目还是web项目
      2. 查找并加载所有可用初始化器，设置到initializers属性中
      3. 找出所有的应用监听器，设置到listener属性中
      4. 推断并设置main方法的定义类，找到运行的主类。
