#### 【1】Linux部署

-------------------------

* 文件下载与解压

  nexus-3.26.1-02-unix.tar.gz

  解压到 /usr/local 下，建立nexus文件夹

  ```shell
  - nexus-3.26.1-02
  - sonatype-work
  ```

* 配置环境变量

  vim /etc/profile

  ```shell
  export RUN_AS_USER=root
  export JAVA_HOME=/usr/local/software/jdk1.8.0_66
  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
  export PATH=.:$JAVA_HOME/bin:$RUN_AS_USER:$PATH
  ```

  source /etc/profile 

* 启动

  nexus start

