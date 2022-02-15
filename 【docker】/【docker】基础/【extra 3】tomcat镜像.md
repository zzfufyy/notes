#### tomcat镜像制作

-------------------

* 步骤

  1. 准备压缩包

  <img src="imgs/截屏2021-06-16 下午6.19.06.png" style="zoom:67%;" />

  2. 编写Dockerfile

     官方命名就是**Dockerfile**

     build会自动寻找这个文件，就不需要-f指定了。

     ```dockerfile
     FROM centos
     MAINTAINER zyw<278496680@qq.com>
     COPY readme.txt /usr/local/readme.txt
     ADD jdk-8ull-linux-x64.tar.gz
     ADD apache-tomcat-9.0.22.tar.gz
     
     RUN yum -y install vim
     
     ENV MYPATH /usr/local
     WORK $MYPATH
     
     ENV JAVA_HOME /usr/local/jdk1.8.0_11
     ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
     ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.22
     ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.22
     ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin
     
     EXPOSE 8080
     CMD /usr/local/apache-tomcat-9.0.22/bin/startup.sh && tail -F /url/local/apache-tomcat-9.0.22/bin/logs/catalina.out
     ```

  3. 构建镜像、启动镜像

     ```shell
     docker build -t diytomcat .
     
     # 运行
     docker run -d -p 9090:8080 --name zywtomcat \
     -v /home/zyw/build/tomcat/test:/usr/local/apache-tomcat-9.0.22/webapps/test\
     -v /home/zyw/build/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.22/logs mytomcat
     ```

  4. 访问测试

     ```shell
     curl localhost:9090
     ```

  5. 发布项目

     由于做了卷挂载，所以可以在本地直接发布项目