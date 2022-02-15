#### docker常用命令

-------------

* 帮助命令

  ```shell
  docker version		# 显示docker版本信息
  docker info				# docker系统信息， 包括镜像和容器
  docker 命令 --help	# 帮助命令
  ```

  帮助文档地址：

  官网reference

* 镜像命令

  - docker images

    查看本机所有镜像

  - docker search   

    搜索镜像

    docker search --filter=stars=3000   

    大于3000 stars的镜像

  - docker pull 镜像名[:tag]

    下载镜像

    docker pull mysql   

    **等价于**  docker pull docker.io/library/mysql:latest

    <img src="imgs/截屏2021-06-07 下午2.30.09.png" style="zoom:67%;" />

    **docker分层下载**

    数字签名

    真实地址： docker.io/library/mysql:5.7

  - docker rmi 删除镜像

    docker rmi -f  镜像id1 id2 ....    

    docker rmi -f $(doc images -aq)   删除所有镜像

* 容器命令

  - Dokcer run [可选参数]  image

    参数说明：

    - --name="Name"   为容器取名

    - -d  后台方式运行

    - -it 使用交互方式运行

    - -p 指定容器端口

      - ip:主机端口:容器端口

      - -p 主机端口：容器端口 （最常用）
      - -p 容器端口
      - 容器端口

    - -P 随机指定端口

    - <img src="imgs/截屏2021-06-08 上午11.46.28.png" style="zoom:80%;" />

    `docker run -it centos /bin/bash`

    退出容器 直接停止:
    
    `exit`
    
    **退出容器，不停止：**
    
    **Ctrl + p + q**
    
  - docker ps  正在运行的容器

    参数：

    -a    正在运行和历史运行的容器

    -n=? 显示最近创建的容器

    -q   显示编号

  - 删除容器

    docker rm  容器id

    docker rm  -f $(docker ps -aq)       删除所有容器id

    docker stop 容器id

    docker start 容器id

    docker pause 容器id

    docker kill  强制停止容器id

    先停再删除

* 进入当前正在运行的容器

  - docker exec -it 容器id bashshell

    docker exec -it c3b305982b80 /bin/bash

    开启一个新的终端

  - docker attach 容器id bashshell

    docker attach c3b305982b80 /bin/bash

    进入当前容器正在运行的终端，不会开启新的进程

* 拷贝容器文件到主机上

  docker cp 容器id: 容器内路径  目的主机路径

  docker cp c3b305982b80:/tmp.txt ./

  拷贝是一个手动过程，一般使用-v 卷的技术，实现容器内目录与主机目录

  同步

* 常用其他命令

  - 后台启动容器

    docker ps -d centos

    容器使用后台运行，就必须要一个前台进程。docker发现没有应用，会自动停止。

    docker run -d centos /bin/sh -c "while true;do echo zyw;done"

  - 查看日志命令

    docker logs -tf --tail 10 容器id

    -t 显示时间戳

    -f 跟随output

  - 查看容器中的进程信息

    dokcer top 容器id

  - 查看容器信息

    docker inspect 容器id

* 端口暴露的概念

  <img src="imgs/截屏2021-06-08 下午4.32.02.png" style="zoom:67%;" />

