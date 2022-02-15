#### 【2】Nexus工程配置

------------------------------------------

* 环境用户maven settings.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <settings xmlns="http://maven.apache.org/SETTINGS/1.1.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
  
      <localRepository>D:\env_programming\repository_mvn</localRepository>
      <interactiveMode/>
      <usePluginRegistry/>
      <offline/>
      <pluginGroups/>
      <servers>
          <server>
              <id>releases</id>
              <username>admin</username>
              <password>admin123</password>
          </server>
          <server>
              <id>snapshots</id>
              <username>admin</username>
              <password>admin123</password>
          </server>
      </servers>
      <mirrors>
          <mirror>
              <id>alimaven</id>
              <mirrorOf>central</mirrorOf>
              <name>aliyun maven</name>
              <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
          </mirror>
      </mirrors>
      <proxies>
          <!--代理元素包含配置代理时需要的信息 -->
          <!--代理的唯一定义符，用来区分不同的代理元素。 -->
          <proxy>
              <id>zteproxy</id>
              <active>true</active>
              <protocol>http</protocol>
              <host>proxysz.zte.com.cn</host>
              <port>80</port>
              <nonProxyHosts>10.*.*.*|*.zte.com.cn|192.*.*.*|127.0.0.1</nonProxyHosts>
          </proxy>
          <proxy>
              <id>ztesproxy</id>
              <active>true</active>
              <protocol>https</protocol>
              <host>proxysz.zte.com.cn</host>
              <port>80</port>
              <nonProxyHosts>10.*.*.*|*.zte.com.cn|192.*.*.*|127.0.0.1</nonProxyHosts>
          </proxy>
      </proxies>
      <profiles/>
      <activeProfiles/>
  
  
  </settings>
  ```

* 工程pom.xml配置

  ```xml
  <distributionManagement>
          <repository>
              <id>releases</id>
              <name>releases</name>
              <url>http://127.0.0.1:8081/repository/maven-releases/</url>
          </repository>
          <snapshotRepository>
              <id>snapshots</id>
              <name>snapshots</name>
              <url>http://127.0.0.1:8081/repository/maven-snapshots/</url>
          </snapshotRepository>
      </distributionManagement>
  ```

  