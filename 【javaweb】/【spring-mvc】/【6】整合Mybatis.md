### 整合Mybatis

-----------

#### 1. Mybatis回顾

- 步骤

  1. 导入相关jar包

     - junit
     - mybatis
     - mysql数据库
     - spring相关的
     - aop植入
     - mybatis-spring

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <project xmlns="http://maven.apache.org/POM/4.0.0"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         <parent>
             <artifactId>spring-test1</artifactId>
             <groupId>com.kuang</groupId>
             <version>1.0-SNAPSHOT</version>
         </parent>
         <modelVersion>4.0.0</modelVersion>
         <artifactId>spring-mybatis</artifactId>
     
         <properties>
             <maven.compiler.source>8</maven.compiler.source>
             <maven.compiler.target>8</maven.compiler.target>
         </properties>
         <dependencies>
             <dependency>
                 <groupId>junit</groupId>
                 <artifactId>junit</artifactId>
                 <version>4.13</version>
                 <scope>test</scope>
             </dependency>
             <dependency>
                 <groupId>mysql</groupId>
                 <artifactId>mysql-connector-java</artifactId>
                 <version>5.1.47</version>
             </dependency>
             <dependency>
                 <groupId>org.mybatis</groupId>
                 <artifactId>mybatis</artifactId>
                 <version>3.5.7</version>
             </dependency>
             <dependency>
                 <groupId>org.springframework</groupId>
                 <artifactId>spring-webmvc</artifactId>
                 <version>5.2.16.RELEASE</version>
             </dependency>
             <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
             <dependency>
                 <groupId>org.aspectj</groupId>
                 <artifactId>aspectjweaver</artifactId>
                 <version>1.9.7</version>
                 <scope>runtime</scope>
             </dependency>
     
             <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
             <dependency>
                 <groupId>org.mybatis</groupId>
                 <artifactId>mybatis-spring</artifactId>
                 <version>2.0.6</version>
             </dependency>
             <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
             <dependency>
                 <groupId>org.projectlombok</groupId>
                 <artifactId>lombok</artifactId>
                 <version>1.18.22</version>
                 <scope>provided</scope>
             </dependency>
         </dependencies>
     
         <build>
             <resources>
                 <resource>
                     <directory>src/main/resources</directory>
                     <includes>
                         <include>**/*.xml</include>
                     </includes>
                 </resource>
             </resources>
         </build>
     
     </project>
     ```

  2. 编写配置文件
  3. 测试

- Mybatis

  1. 编写实体类
  2. 编写核心配置文件
  3. 编写接口
  4. 编写Mapper.xml
  5. 测试

- 实例

  <img src="imgs/截屏2021-10-13 下午11.03.01.png" alt="截屏2021-10-13 下午11.03.01" style="zoom:50%;" />

  - Mybatis-config.xml

    **特别注意useSSL需要是false**

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    
    <!-- configuration 核心配置文件-->
    <configuration>
        <typeAliases>
            <package name="com.kuang.pojo"/>
        </typeAliases>
    
        <environments default="development">
            <environment id="development">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
                    <property name="driver" value="com.mysql.jdbc.Driver"/>
                    <property name="url" value="jdbc:mysql://localhost:3306/jdbc?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                    <property name="username" value="root"/>
                    <property name="password" value="123456"/>
                </dataSource>
            </environment>
        </environments>
    
        <mappers>
            <mapper class="com.kuang.mapper.UserMapper"/>
        </mappers>
    </configuration>
    ```

  - Mapper类

    ```java
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import java.util.List;
    
    public interface UserMapper {
        public List<User> selectUser();
    }
    ```

  - pojo类

    ```java
    package com.kuang.pojo;
    import lombok.Data;
    import java.util.Date;
    
    @Data
    public class User {
        private int id;
        private String name;
        private String password;
        private String email;
        private Date birthday;
    }
    
    ```

  - mapper的xml

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    
    <mapper namespace="com.kuang.mapper.UserMapper">
        <select id="selectUser" resultType="user">
            select * from jdbc.user;
        </select>
    </mapper>
    ```

----------------------------

#### 2. 整合mybatis方式（一）

- 理解

  - 允许Mybatis参与到Spring的事务管理当中
  - 创建映射器mapper和Sqlsession注入到bean中。
  - 将Mybatis的异常转换为Spring的DataAcessException。

- 步骤

  - applicationContext.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <import resource="spring-dao.xml"/>
        <bean id="userMapper" class="com.kuang.mapper.UserMapperImpl">
            <property name="sqlSession" ref="sqlSession"/>
        </bean>
    </beans>
    ```

    

  - mybatis-config.xml配置

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    
    <!-- configuration 核心配置文件-->
    <configuration>
        <typeAliases>
            <package name="com.kuang.pojo"/>
        </typeAliases>
    </configuration>
    ```

  - spring-dao.xml配置

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
        <!--  使用Spring的数据源替换Mybatis  c3p0 dbcp druid
            这里使用spring提供的jdbc
    
        -->
        <bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
            <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql://localhost:3306/jdbc?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </bean>
    
        <!--  sqlSessionFactory  -->
        <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
            <property name="dataSource" ref="datasource"/>
            <!--   绑定Mybatis配置文件     -->
            <property name="configLocation" value="classpath:mybatis-config.xml"/>
            <property name="mapperLocations" value="classpath:com/kuang/mapper/*.xml"/>
        </bean>
    
        <!-- sqlsessionTemplate 就是sqlSession  -->
        <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
            <!--  只能使用构造器注入sqlSessionFactory      -->
            <constructor-arg index="0" ref="sqlSessionFactory"/>
        </bean>
    
    </beans>
    ```

  - Mapper接口

    ```java
    //
    // Source code recreated from a .class file by IntelliJ IDEA
    // (powered by FernFlower decompiler)
    //
    
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import java.util.List;
    
    public interface UserMapper {
        List<User> selectUser();
    }
    
    ```

  - Mapper实现类

    ```java
    //
    // Source code recreated from a .class file by IntelliJ IDEA
    // (powered by FernFlower decompiler)
    //
    
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import java.util.List;
    import org.mybatis.spring.SqlSessionTemplate;
    
    public class UserMapperImpl implements UserMapper {
        private SqlSessionTemplate sqlSession;
    
        public UserMapperImpl() {
        }
    
        public void setSqlSession(SqlSessionTemplate sqlSession) {
            this.sqlSession = sqlSession;
        }
    
        public List<User> selectUser() {
            UserMapper mapper = (UserMapper)this.sqlSession.getMapper(UserMapper.class);
            return mapper.selectUser();
        }
    }
    ```

  - Mapper映射文件

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN" 
    							 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    
    <mapper namespace="com.kuang.mapper.UserMapper">
        <select id="selectUser" resultType="com.kuang.pojo.User">
            select * from jdbc.user;
        </select>
    </mapper>
    ```

  - 附：UserPojo使用@Data编译好文件

    ```java
    //
    // Source code recreated from a .class file by IntelliJ IDEA
    // (powered by FernFlower decompiler)
    //
    
    package com.kuang.pojo;
    
    import java.util.Date;
    
    public class User {
        private int id;
        private String name;
        private String password;
        private String email;
        private Date birthday;
    
        public User() {
        }
    
        public int getId() {
            return this.id;
        }
    
        public String getName() {
            return this.name;
        }
    
        public String getPassword() {
            return this.password;
        }
    
        public String getEmail() {
            return this.email;
        }
    
        public Date getBirthday() {
            return this.birthday;
        }
    
        public void setId(int id) {
            this.id = id;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public void setPassword(String password) {
            this.password = password;
        }
    
        public void setEmail(String email) {
            this.email = email;
        }
    
        public void setBirthday(Date birthday) {
            this.birthday = birthday;
        }
    
        public boolean equals(Object o) {
            if (o == this) {
                return true;
            } else if (!(o instanceof User)) {
                return false;
            } else {
                User other = (User)o;
                if (!other.canEqual(this)) {
                    return false;
                } else if (this.getId() != other.getId()) {
                    return false;
                } else {
                    label61: {
                        Object this$name = this.getName();
                        Object other$name = other.getName();
                        if (this$name == null) {
                            if (other$name == null) {
                                break label61;
                            }
                        } else if (this$name.equals(other$name)) {
                            break label61;
                        }
    
                        return false;
                    }
    
                    label54: {
                        Object this$password = this.getPassword();
                        Object other$password = other.getPassword();
                        if (this$password == null) {
                            if (other$password == null) {
                                break label54;
                            }
                        } else if (this$password.equals(other$password)) {
                            break label54;
                        }
    
                        return false;
                    }
    
                    Object this$email = this.getEmail();
                    Object other$email = other.getEmail();
                    if (this$email == null) {
                        if (other$email != null) {
                            return false;
                        }
                    } else if (!this$email.equals(other$email)) {
                        return false;
                    }
    
                    Object this$birthday = this.getBirthday();
                    Object other$birthday = other.getBirthday();
                    if (this$birthday == null) {
                        if (other$birthday != null) {
                            return false;
                        }
                    } else if (!this$birthday.equals(other$birthday)) {
                        return false;
                    }
    
                    return true;
                }
            }
        }
    
        protected boolean canEqual(Object other) {
            return other instanceof User;
        }
    
        public int hashCode() {
            int PRIME = true;
            int result = 1;
            int result = result * 59 + this.getId();
            Object $name = this.getName();
            result = result * 59 + ($name == null ? 43 : $name.hashCode());
            Object $password = this.getPassword();
            result = result * 59 + ($password == null ? 43 : $password.hashCode());
            Object $email = this.getEmail();
            result = result * 59 + ($email == null ? 43 : $email.hashCode());
            Object $birthday = this.getBirthday();
            result = result * 59 + ($birthday == null ? 43 : $birthday.hashCode());
            return result;
        }
    
        public String toString() {
            return "User(id=" + this.getId() + ", name=" + this.getName() + ", password=" + this.getPassword() + ", email=" + this.getEmail() + ", birthday=" + this.getBirthday() + ")";
        }
    }
    
    ```

  - 测试

    ```java
    import com.kuang.mapper.UserMapper;
    import com.kuang.pojo.User;
    import org.junit.Test;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    import java.io.IOException;
    
    public class MyTest {
        @Test
        public void test() throws IOException {
            ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
            UserMapper userMapper = context.getBean("userMapper",UserMapper.class);
            for(User user : userMapper.selectUser()){
                System.out.println(user);
            }
        }
    }
    
    ```

-------------

#### 3. 整合Mybatis方式（二）

- 理解

  - 所有操作，都是使用sqlSession来执行。在原来都使用SqlSessionTemplate

- 步骤

  - UserMapperImpl2

    ```java
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import org.apache.ibatis.session.SqlSession;
    import org.mybatis.spring.support.SqlSessionDaoSupport;
    
    import java.util.List;
    
    public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
        @Override
        public List<User> selectUser() {
            SqlSession sqlSession = getSqlSession();
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);
            return getSqlSession().getMapper(UserMapper.class).selectUser();
        }
    }
    
    ```

  - applicationContext.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <import resource="spring-dao.xml"/>
        <bean id="userMapper" class="com.kuang.mapper.UserMapperImpl">
            <property name="sqlSession" ref="sqlSession"/>
        </bean>
    
        <bean id="userMapper2" class="com.kuang.mapper.UserMapperImpl2">
            <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
        </bean>
    
    </beans>
    ```

-------------

#### 4. spring声明事务

- 事务

  - 一组业务当成一个业务来做，要么都成功，要么都失败
  - 事务在项目开发中，十分重要，涉及到数据的一致性问题
  - 确保完整性和一致性

- 事务AICD原则

  - 原子性
  - 一致性
  - 隔离性
    - 多个业务可能操作同一个资源，防止数据损坏。
  - 持久性
    - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响，被持久化的写到存储器。

- Mybatis事务管理

  - mybatis-spring的一个优势是，它允许Mybatis参与到Spring的事务管理。

    而不是给Mybatis创建一个新的专用事务管理器。

    **DataSourceTransactionManager**

  - 标准配置

    ```xml
    <bean id="transactionManager" 
    ```

- Spring中的事务管理

  - 声明式事务：AOP
  - 编程式事务：需要在代码中，进行事务管理。

- 代码

  - applicationContext.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <import resource="spring-dao.xml"/>
        <bean id="userMapper" class="com.kuang.mapper.UserMapperImpl">
            <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
        </bean>
    </beans>
    ```

  - mybatis-config.xml

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    
    <!-- configuration 核心配置文件-->
    <configuration>
        <typeAliases>
            <package name="com.kuang.pojo"/>
        </typeAliases>
    </configuration>
    ```

  - Spring-dao.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:tx="http://www.springframework.org/schema/tx" xmlns:aop="http://www.springframework.org/schema/aop"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/tx
                http://www.springframework.org/schema/tx/spring-tx.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">
        <!--  使用Spring的数据源替换Mybatis  c3p0 dbcp druid
            这里使用spring提供的jdbc
    
        -->
        <bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
            <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql://localhost:3306/jdbc?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </bean>
    
        <!--  sqlSessionFactory  -->
        <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
            <property name="dataSource" ref="datasource"/>
            <!--   绑定Mybatis配置文件     -->
            <property name="configLocation" value="classpath:mybatis-config.xml"/>
            <property name="mapperLocations" value="classpath:com/kuang/mapper/*.xml"/>
        </bean>
    
        <!-- sqlsessionTemplate 就是sqlSession  -->
        <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
            <!--  只能使用构造器注入sqlSessionFactory      -->
            <constructor-arg index="0" ref="sqlSessionFactory"/>
        </bean>
    
    
        <!--  配置声明式事务管理  -->
        <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
            <property name="dataSource" ref="datasource"/>
        </bean>
    
        <!-- 结合AOP实现事务的织入   -->
        <!--  配置事务的类：  -->
        <!--  配置事务通知  -->
        <tx:advice id="txAdvice" transaction-manager="transactionManager">
            <!--  给那些方法配置事务      -->
            <!--  配置事务的传播特性  默认required -->
            <tx:attributes>
                <tx:method name="add" propagation="REQUIRED"/>
                <tx:method name="delete"/>
                <tx:method name="update"/>
                <tx:method name="query" read-only="true"/>
                <tx:method name="*"/>
            </tx:attributes>
        </tx:advice>
    
        <aop:config>
            <aop:pointcut id="txPointCut" expression="execution(* com.kuang.mapper.*.*(..))"/>
            <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
        </aop:config>
    </beans>
    ```

  - UserMapper.xml

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    
    <mapper namespace="com.kuang.mapper.UserMapper">
        <select id="selectUser" resultType="com.kuang.pojo.User">
            select * from jdbc.user;
        </select>
    
        <insert id="addUser" parameterType="user">
            insert  into jdbc.user(id,name,password,email) values(#{id},#{name},#{password},#{email});
        </insert>
    
        <delete id="deleteUser" parameterType="int">
            delete from jdbc.user where id=#{id}
        </delete>
    </mapper>
    ```

  - User.java

    ```java
    package com.kuang.pojo;
    
    import lombok.AllArgsConstructor;
    import lombok.Data;
    import lombok.NoArgsConstructor;
    
    import java.util.Date;
    
    @Data
    @AllArgsConstructor
    @NoArgsConstructor
    public class User {
        private int id;
        private String name;
        private String password;
        private String email;
    }
    
    ```

  - UserMapper.java

    ```java
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import java.util.List;
    
    public interface UserMapper {
        public List<User> selectUser();
        public int addUser(User user);
        public int deleteUser(int id);
    }
    
    ```

  - UserMapperImpl.java

    ```java
    package com.kuang.mapper;
    
    import com.kuang.pojo.User;
    import org.apache.ibatis.session.SqlSession;
    import org.mybatis.spring.support.SqlSessionDaoSupport;
    
    import java.util.Date;
    import java.util.List;
    
    public class UserMapperImpl extends SqlSessionDaoSupport implements UserMapper {
        @Override
        public List<User> selectUser() {
    
            User user = new User(5, "小王", "123456", "tmp@qq.com");
    
            UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
            System.out.println(mapper.deleteUser(5));
            System.out.println(mapper.addUser(user));
    
            return mapper.selectUser();
    
        }
    
        @Override
        public int addUser(User user) {
            return getSqlSession().getMapper(UserMapper.class).addUser(user);
        }
    
        @Override
        public int deleteUser(int id) {
            return getSqlSession().getMapper(UserMapper.class).deleteUser(id);
        }
    }
    
    
    ```

  - MyTest.java

    ```java
    import com.kuang.mapper.UserMapper;
    import com.kuang.pojo.User;
    import org.junit.Test;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    import java.io.IOException;
    
    public class MyTest {
        @Test
        public void test() throws IOException {
            ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
            UserMapper userMapper = context.getBean("userMapper",UserMapper.class);
            for(User user : userMapper.selectUser()){
                System.out.println(user);
            }
        }
    }
    ```

- 

  
