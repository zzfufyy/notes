#### Maven

---------

* Maven   项目架构管理工具

  见IDE软件中MAVEN。

* Maven项目构建

  实际上需要的如下：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  	
    <!-- 配置的GAV -->
    <groupId>com.zyw</groupId>
    <artifactId>javaweb-01-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
  	<!-- 打包方式： jar java应用   war  web应用-->
    <packaging>war</packaging>
  
  <!-- 实际不需要
    <name>javaweb-01-maven Maven Webapp</name>
    <url>http://www.example.com</url>
  -->
    <!-- 配置 -->
    <properties>
      <!-- 编码 -->
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  		<!-- 编译版本 -->    
      <maven.compiler.source>1.8</maven.compiler.source>
      <maven.compiler.target>1.8</maven.compiler.target>
    </properties>
  	
    <!-- 依赖包 -->
    <!-- maven的高级之处会帮助你导入这个jar包所依赖的其他jar包-->
    <dependencies>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.11</version>
        <scope>test</scope>
      </dependency>
    </dependencies>
  
  	<!-- 构建工具，一般idea中模板生成默认会带有这些构建插件等 -->  
    <build>
      <!-- 配置resources 来防止资源到处失败的问题 -->
     	<resources>
      	<resource>
        	<directory>
          	src/main/resources
          </directory>
          <excludes>
          	<exclude>**/*.properties</exclude>
            <exclude>**/*.xml</exclude>
          </excludes>
          <filtering>false</filtering>
        </resource>
          <resource>
          	<directory>
              src/main/java
            	<includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
              </includes>
              <filtering>false</filtering>
            </directory>
          </resource>
      </resources>
      
      <finalName>javaweb-01-maven</finalName>
      <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
        <plugins>
          <plugin>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.1.0</version>
          </plugin>
         	......
        </plugins>
      </pluginManagement>
    </build>
  </project>
  
  ```

  

  

