#### 图形化管理工具

----------------

* Portainer

  Docker图形化界面管理工具，提供一个后台面板供我们操作

  - 下载

    ```shell
    docker run -d -p 8088:9000\
    --restart=always -v /var/run/docker.sock:/var/run/docker.sock\
    --priviliged=true portainer/po
    ```

    