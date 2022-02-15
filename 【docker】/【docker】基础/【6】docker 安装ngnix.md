#### docker安装nginx

--------------------

* 基础安装

  - dockerhub搜索资源  nginx，找到版本号和相关 镜像的说明

  - 搜索

    docker search nginx

  - 拉取

    docker pull nginx

    docker pull docker.io/library/nginx:latest

  - 运行

    docker run -d --name nginx01 -p 3344:80 nginx

  - 效果

    本机3344可打开，localhost:3344

    <img src="imgs/截屏2021-06-08 下午4.35.24.png" style="zoom:80%;" />

