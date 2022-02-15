### SpringBoot Web开发

-----------

#### 1. 思路

- 要解决的问题
  1. 导入静态资源
  2. 首页
  3. jsp-> 模板引擎 Thymeleaf
  4. 装配拓展   SpringMVC
  5. 增删改查
  6. 拦截器
  7. 国际化

----

#### 2. ThymeLeaf 模板引擎

[**链接 - thymeleaf帮助文档**](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html)

- 导入静态资源
  - webjars
  - public, static, /** , resourecs      localhost:8080/
  - 优先级：resources  > static(默认) > public 

- 引入模板引擎

  ```xml
  <!--	Thymeleaf 3.x	-->
  <dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring5</artifactId>
  </dependency>
  <dependency>
    <groupId>org.thymeleaf.extras</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
  </dependency>
  
  ```

  - IndexController.java

    ```java
    package com.kuang.springbootdemo.controller;
    
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.RequestMapping;
    
    @Controller
    public class IndexController {
    
        @RequestMapping("/test")
        public String test(Model model) {
            model.addAttribute("msg", "hello, SPRINGboot");
            return "test";
        }
    }
    
    ```

  - templates文件夹下面建立test.html

    ```html
    <!DOCTYPE html>
    <html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <h1>thymeleaf测试</h1>
        <!-- 所有html元素都可以被接管，th:元素名   -->
        <h2 th:text="${msg}"></h2>
    </body>
    </html>
    ```

- Thymeleaf语法

  - ${} 变量
  - *{}  ex表达式
  - #{}  消息
  - @{}  URL
  - ~{}   Fragment Expression