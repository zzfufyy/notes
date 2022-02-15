### Spring基础

------------

#### 1. 简介

- spring理念

  目的：解决企业开发的复杂性。

  本身是一个大杂烩。

  向后兼容性。

- SSH 

  Struct2 + spring + hibernate

- SSM

  springMVC + spring +mybatis

- 需要依赖
  - org.springframework.spring-webmvc
  - org.springframework.spring-jdbc

- 优点
  - spring 是一个开源框架（容器）
  - spring 是一个轻量级的、非入侵式的框架
  - **控制反转 IOC，面向切面编程 AOP**
  - 支持事务处理，对框架整合的支持。

<img src="imgs/截屏2021-08-19 下午4.23.43.png" alt="截屏2021-08-19 下午4.23.43" style="zoom:67%;" />

- **springboot**
  - 快速开发的脚手架
  - 基于springboot可以快速开发单个微服务
  - 约定大于配置！
- **springcloud**
  - 基于springboot实现
  - 分布式

#### 2. Spring配置说明

- bean配置

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

  - id：唯一标识符
  - alias：bean对象的别名
  - class：bean对象  限定类全名
  - name： 别名，可取多个（逗号等分割）

- import配置

  一般用于团队开发，将多个文件合并为一个applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd">
  
        <import resource="bean1.xml"/>
        <import resource="bean2.xml"/>
        <import resource="bean3.xml"/>
  </beans>
  ```

  