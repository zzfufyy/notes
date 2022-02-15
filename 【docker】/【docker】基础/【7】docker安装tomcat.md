#### docker安装tomcat

-----------------

* 基础安装

  - 官方安装命令

    docker run -it --rm tomcat:9.0

    --rm 用完即删除   这种方式仅用于测试

    docker run -d -p 3355:8080 --name tomcat01 tomcat

    docker exec -it tomcat01 /bin/bash

    默认是最小安装，容器中tomcat的webapps中没有任何文件

    