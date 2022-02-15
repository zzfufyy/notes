#### Run流程和Docker原理

------------

* Docker Run运行

  <img src="imgs/截屏2021-06-07 下午1.49.50.png" style="zoom:57%;" />

* 底层原理

  - docker是怎么工作的

    Docker是一个C/S结构的系统，Docker的守护进程运行在主机上。

    通过Socket从客户端访问。

    DockerServer接收到Docker-Client指令，就会执行这个命令。

    <img src="imgs/截屏2021-06-07 下午1.55.12.png" style="zoom:57%;" />

  - Docker为什么比虚拟机块

    - Docker比虚拟机有着更少的抽象层。

      <img src="imgs/截屏2021-06-07 下午1.56.47.png" style="zoom:67%;" />

    - Docker利用的是宿主机的内核，vm需要的是 Guest OS。

    所以说，新建一个容器的时候，Docker不需要重新加载一个操作系统内核。

    虚拟机加载的是Guest OS。

    Docker利用的是宿主机的操作系统。省略了这个复杂的过程。

    <img src="imgs/截屏2021-06-07 下午2.00.44.png" style="zoom:67%;" />

    现在docker都支持全平台。

  