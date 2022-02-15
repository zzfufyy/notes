#### Dockfile

-------------

* 用处

  构建docker镜像的文件，命令参数脚本

  构建步骤：

  1. 编写一个dockerfile文件
  2. docker build 构建称为一个镜像
  3. docker run 运行
  4. docker push  发布

  比如 dockhub centos中，点进去，其实是一个dockerfile：

  ```dockerfile
  FROM scratch
  ADD centos-7-x86_64-docker.tar.xz /
  
  LABEL \
      org.label-schema.schema-version="1.0" \
      org.label-schema.name="CentOS Base Image" \
      org.label-schema.vendor="CentOS" \
      org.label-schema.license="GPLv2" \
      org.label-schema.build-date="20201113" \
      org.opencontainers.image.title="CentOS Base Image" \
      org.opencontainers.image.vendor="CentOS" \
      org.opencontainers.image.licenses="GPL-2.0-only" \
      org.opencontainers.image.created="2020-11-13 00:00:00+00:00"
  
  CMD ["/bin/bash"]
  ```

* 基础知识

  1. 关键字必须大写

  2. 执行从上到下

  3. \# 表示注释

  4. **每一个指令都会创建提交一个新的镜像层，并提交**

     <img src="imgs/截屏2021-06-16 下午3.38.29-3829392.png" style="zoom:67%;" />

  dockerfile是面向开发的，以后要发布项目，做镜像，就需要编写dokcerfile，这个文件十分简单。

  Docker镜像，逐渐称为了企业交付的标准。

  dockerfile - 构建文件。定义了一切的步骤，源代码

  dockerimages：通过dockerfile构建生成镜像，最终发布和运行的产品

  docker容器：镜像运行起来提供服务器。

* dockerfile 命令

  <img src="imgs/截屏2021-06-16 下午3.49.23.png" style="zoom:67%;" />

  ```dockerfile
  FROM        # 基础镜像
  MAINTAINER  # 镜像是谁写的，姓名 + 邮箱
  RUN         # 镜像构建的时候需要运行的命令
  ADD         # 步骤：tomcat镜像， tomcat 压缩包！ 添加内容
  WORKDIR     # 镜像的工作目录
  VOLUME      # 挂载的容器卷
  EXPOSE      # 指定暴露端口
  CMD         # 指定容器启动的时候要运行的命令,只有最后一个会生效，可被替代
  ENTRYPOINT  # 指定容器启动的时候要运行的命令，可以追加命令
  ONBUILD     # 当构建一个被继承的dockerfile，这个时候会运行ONBUILD指令。
  COPY        # 复制 类似ADD，将文件拷贝到镜像中。
  ENV         # 构建的时候设置环境变量
  
  ```

* 发布镜像

  - dockerhub上注册账号

  - 终端上登录账号 

    ```shell
    docker login -u zyw
    Password:
    ```

  - push镜像

    ```shell
    # 需要带版本号，打tag，
    不然会被拒绝
    docker tag f8559daf1fc2 zyw/tomcat:1.0
    docker push zyw/ditomcat:0.1
    
    ```

    