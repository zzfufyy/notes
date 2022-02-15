#### 实践 spring boot 微服务

-------------

* 构建springboot项目

  intelliJ构建，

  打包成jar

* 发布到dockerfile中

  idea中装插件  docker integration

* 写Dockerfile

  ```dockerfile
  FROM java:8
  
  # 拷贝到jar
  COPY *.jar /app.jar
  
  # 设置参数
  CMD ["--server.port=8080"]
  
  EXPOSE 8080
  
  # 执行
  ENTRYPOINT ["java","-jar","/app.jar"]
  ```

* 构建docker

  jar包和Dockerfile同一目录

  ```shell
  # 构建镜像
  docker build -t kuangshen666
  
  # 启动
  docker run -d -P --name kuangshen-springboot-web kuangshen666
  
  # 测试
  curl localhost:32770/hello
  ```