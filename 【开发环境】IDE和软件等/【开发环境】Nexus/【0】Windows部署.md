#### 【0】Windows部署Nexus

------------------------

* 下载

  nexus-3.22.1-02-win64.zip

* 配置环境变量

  %NEXUS_HOME% : ..\nexus-3.22.1-02-win64\nexus-3.22.1-02

  PATH += %NEXUS_HOME%\bin

* 启动

  ```shell
  nexus
  nexus -h
  nexus.exe/start
  ```

* 界面

  nexus-3.22.1-02-win64\sonatype-work\nexus3\etc  下 nexus.properties文件为  配置文件。

  ```properties
  # Jetty section
  application-port=8081
  application-host=0.0.0.0
  nexus-args=${jetty.etc}/jetty.xml,${jetty.etc}/jetty-http.xml,${jetty.etc}/jetty-requestlog.xml
  nexus-context-path=/
  
  # Nexus section
  nexus-edition=nexus-pro-edition
  nexus-features=\
  nexus-pro-feature
  
  # nexus.hazelcast.discovery.isEnabled=true
  
  ```

  改成 127.0.0.1

  nexus-3.22.1-02-win64\sonatype-work\nexus3 下 admin.properties 为初始密码

  <img src="%E3%80%900%E3%80%91windows%E9%83%A8%E7%BD%B2.assets/2020-09-02_134429.png" style="zoom:75%;" />

  