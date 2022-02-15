### 【vs-java】配置springweb基本开发环境.md

----------------------------------

* 配置maven settings（特制公司）

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <settings xmlns="http://maven.apache.org/SETTINGS/1.1.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
  
      <localRepository/>
      <interactiveMode/>
      <usePluginRegistry/>
      <offline/>
      <pluginGroups/>
      <servers>
          <server>
              <id>zte</id>
          </server>
      </servers>
      <!--为仓库列表配置的下载镜像列表。  -->
      <mirrors>
          <!--给定仓库的下载镜像。  -->
          <!--该镜像的唯一标识符。id用来区分不同的mirror元素。  -->
          <!--根据镜像所在地址，可设置为https://artnj.zte.com.cn、https://artxa.zte.com.cn等 -->
     <!--      <mirror>
              <id>zte</id>
              <mirrorOf>*</mirrorOf>
              <url>https://artsz.zte.com.cn/artifactory/public-maven-virtual/</url>
          </mirror> -->
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
              <host>proxynj.zte.com.cn</host>
              <port>80</port>
              <nonProxyHosts>10.*.*.*|*.zte.com.cn|192.*.*.*|127.0.0.1</nonProxyHosts>
          </proxy>
          <proxy>
              <id>ztesproxy</id>
              <active>true</active>
              <protocol>https</protocol>
              <host>proxynj.zte.com.cn</host>
              <port>80</port>
              <nonProxyHosts>10.*.*.*|*.zte.com.cn|192.*.*.*|127.0.0.1</nonProxyHosts>
          </proxy>
      </proxies>
      <profiles/>
      <activeProfiles/>
  
  </settings>
  ```

  

* vscode  settings 中 java配置

  ```json
    // java CONFIG
      "java.semanticHighlighting.enabled": true,
      "java.errors.incompleteClasspath.severity": "ignore",
      "java.configuration.checkProjectSettingsExclusions": false,
      "java.home": "D:\\env_programming\\env_java\\1.8",
      "java.jdt.ls.vmargs": "-noverify -Xmx1G -XX:+UseG1GC -XX:+UseStringDeduplication",
  ```

* vscode settings 中 maven 配置

  ```
  ![2020-06-03_145937](..\【素材】笔记图片源\2020-06-03_145937.png) "maven.executable.path": "D:\\env_programming\\env_maven\\apache-maven-3.6.1\\bin\\mvn",
      "java.configuration.maven.userSettings": "D:\\env_programming\\env_maven\\apache-maven-3.6.1\\conf\\settings.xml",
      "maven.terminal.useJavaHome": true,
      "maven.terminal.customEnv": [
          {
              "environmentVariable": "JAVA_HOME",
              "value": "D:\\env_programming\\env_java\\1.8"
          }
      ],
  ```

* 配置tomcat

  ![](..\【素材】笔记图片源\2020-06-03_145937.png)

* 下载spring插件

  ![spring boot extension pack](..\【素材】笔记图片源\2020-06-03_144949.png)

* 创建

  ctrl + shift + p 

  ![](..\【素材】笔记图片源\2020-06-03_145433.png)

  ![](..\【素材】笔记图片源\2020-06-03_145552.png)

  创建Controller

  <img src="..\【素材】笔记图片源\2020-06-03_145656.png" style="zoom:70%;" />

* 配置launch.json

  ![](..\【素材】笔记图片源\2020-06-03_145820.png)

* 启动

  <img src="..\【素材】笔记图片源\2020-06-03_150222.png" style="zoom:75%;" />

* 页面

  映射/test

  ![](..\【素材】笔记图片源\2020-06-03_150313.png)