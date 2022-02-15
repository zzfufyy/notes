#### docker部署ES和kubana

------------------

* 基础安装

  - dockerhub搜索

    官方启动命令：

    ```bash
    docker run -d --name elasticsearch --net somenetwork \
    -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag
    ```

    基础使用：

    ```bash
    docker run -d --name elasticsearch \
    -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.13.1
    ```

    es非常消耗内存

    <img src="imgs/截屏2021-06-09 下午2.28.23.png" style="zoom:80%;" />

    需要增加内存限制，修改配置文件

    -e 环境配置修改

  - 添加配置启动

    ```bash
    docker run -d --name elasticsearch \
    -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" \
    -e ES_JAVA_OPTS="-Xms64m -Xmx512m" \
    elasticsearch:7.13.1
    ```

    <img src="imgs/截屏2021-06-09 下午2.35.08.png" style="zoom:80%;" />

    <img src="imgs/截屏2021-06-09 下午2.36.03.png" style="zoom:67%;" />

* 思考：kibana连接eS

  <img src="imgs/截屏2021-06-09 下午2.38.12.png" style="zoom:80%;" />