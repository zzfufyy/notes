### springboot配置

------

#### 1. 配置文件

- 官方配置

  springboot使用一个全局配置文件

  Application.properties

  - key=value

  application.yaml

  - key =空格 value

- yaml

  ```yaml
  # 对空格的要求很高
  server:
  	port: 8080
  
  # 行内写法
  student: {name: qingjiang,age: 3}
  
  # 数组
  pets: 
  	- cat
  	- dog
  	- pig
  pets: [cat,dog,pig]
  ```

  - yaml扩展

    ```yaml
    person:
    	name: zyw${random.uuid}
    	age: ${random.int}
    # 占位符
    name: ${person.hello:hello}_旺财  # 如果存在为hello 否则为旺财
    ```

  - 松散绑定

    比如yaml中的 last-name   对应的是 lastName，这是一样的，后面跟着的字母默认是大写。

  - JR303数据校验

    在字段增加一层过滤器验证，可以保证数据的合法性

    ```java
    @Valudated
    public class Person{
      @Email(message="邮箱格式错误OaO ")
      private String name; // 如果不是邮箱格式，会报错
    }
    ```

    

  - 复杂类型封装

    yaml可以封装对象，@value不支持。

    

- 实例

  - Dog.java

    ```java
    package com.kuang.springboottest.pojo;
    
    import lombok.AllArgsConstructor;
    import lombok.Data;
    import lombok.NoArgsConstructor;
    
    @Data
    @AllArgsConstructor
    @NoArgsConstructor
    public class Dog {
        private String name;
        private Integer age;
    }
    
    ```

  - Person

    ```java
    package com.kuang.springboottest.pojo;
    
    import lombok.AllArgsConstructor;
    import lombok.Data;
    import lombok.NoArgsConstructor;
    import org.springframework.boot.context.properties.ConfigurationProperties;
    import org.springframework.stereotype.Component;
    
    import java.util.Date;
    import java.util.List;
    import java.util.Map;
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    @Component
    @ConfigurationProperties(prefix = "person1")
    // 指定配置文件
    // @PropertySource(value = "classpath:qingjiang.properties")
    public class Person {
        private String name;
        private Integer age;
        private boolean happy;
        private Date birth;
        private Map<String, Object> maps;
        private List<Object> lists;
        private Dog dog;
    }
    
    ```

  - Applilcation.yaml

    ```yaml
    person1:
      name: zyw
      age: 3
      happy: false
      birth: 2019/11/2
      maps: {k1: v1, k2: v2}
      lists:
        - code
        - music
        - girl
      dog:
        name: 旺财
        age: 3
    ```

  - 测试入口

    ```java
    package com.kuang.springboottest;
    
    import com.kuang.springboottest.pojo.Person;
    import org.junit.jupiter.api.Test;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.context.SpringBootTest;
    
    // 单元测试
    @SpringBootTest
    class SpringboottestApplicationTests {
    
        @Autowired
        private Person person;
        @Test
        void contextLoads() {
            System.out.println(person);
        }
    
    }
    
    ```

- 多配置文件

  ```yaml
  server:
  	port: 8081
  spring:
  	profiles:
  		active: dev
  ---
  server:
  	port: 8082
  spring:
  	profiles: dev
  ---
  server:
  	port: 8083
  	profiles: test
  ```

------------

#### 2. 配置文件详解

- 配置和 spring.factories

  - xxxAutoConfiguration：    向容器中自动配置组件

  - xxxProperties： 自动配置类，装配配置文件中自定义以诶些内容

  和配置文件绑定，就可以使用自定义的配置了。

  

  

