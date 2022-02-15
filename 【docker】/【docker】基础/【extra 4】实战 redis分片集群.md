

#### 实战 redis分片集群

----------

* redis分片集群

  - 创建网络

  ```shell
  docker network create redis --subnet 172.38.0.0/16
  
  docker network inspect redis
  ```

  - shell脚本创建网卡

  ```bash
  # 创建6个redis配置
  for port in $(seq 1 6);
  do 
  mkdir -p mydata/redis/node-${port}/conf
  touch /mydata/redis/node-${port}/conf/redis.conf
  cat << EOF >/mydata/redos/node-${port}/conf/redis.conf
  port 6379
  bind 0.0.0.0
  cluster-enabled yes
  cluster-config-file nodes.conf 
  cluseter-node-timeout 5000
  cluster-announce-ip 172.38.0.1${port}
  cluster-announce-port 6379
  cluster-announce-bus-port  16379
  appendonly yes
  EOF
  done
  ```

  - 启动

  ```shell
  docker run -p 6371:6379 16371:6379 -p 16371:16379 --name redis-1 \
  -v /mydata/redis/node-1/data:/data \
  -v /mydata/redis/node-1/conf/redis.conf:/etc/redis/redis.conf \
  -d --net redis --ip 172.38.0.11 redis:5.0.9-alpine3.11 \
  redis-server /etc/redis/redis.conf
  
  ....
  6371-6376
  ```

  - 创建集群

  ```shell
  redis-cli --cluster create 172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 172.38.0.15:6379 172.38.0.16:6379 --cluster-replicas 1
  ```

  - 测试

    ```shell
    redis-cli -c 
    set a b
    # 显示 3主3从
    docker stop redis-3 
    # 停止存在的redis-3
    get a
    # 能获取 b
    ```

    

  

  

  

  