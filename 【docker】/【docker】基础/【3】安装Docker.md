安装Docker

---------

- 安装流程

  官网看教程

- 以centos为例

  ```shell
  # 1.卸载旧的版本
   sudo yum remove docker \
                    docker-client \
                    docker-client-latest \
                    docker-common \
                    docker-latest \
                    docker-latest-logrotate \
                    docker-logrotate \
                    docker-engine
  # 2.yum工具包
  sudo yum install -y yum-utils
  
  # 3.设置镜像仓库
  sudo yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo
  # 使用国内镜像仓库
  sudo yum-config-manager \
      --add-repo \
  	 http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
  
  # 4.更新yum索引
  yum makecache fast
  
  # 5. docker-ce社区版本
  yum install docker-ce docker-ce-cli containerd.io
  
  # 6. 查看version
  docker version
  
  # 7. 启动docker服务
  systemctl start docker
  
  # 8. 测试服务
  docker run hello-world
  ```

- 查看镜像

  ```shell
  docker images
  ```

- 卸载docker

  ```shell
  # 1. 卸载依赖
  yum remove docker-ce docker-ce-cli containerd.io
  
  # 2. 删除资源(docker 默认工作路径)
  rm -rf /var/lib/docker
  
  # 3.
  ```

  

- run hello-world说明

  <img src="imgs/截屏2021-06-07 下午1.21.19.png" style="zoom:50%;" />

- 阿里云镜像加速器

  ```shell
  sudo mkdir -p /etc/docker
  sudo tee /etc/docker/daemon.json <<-'EOF'
  {
    "registry-mirrors": ["https://g8j926b8.mirror.aliyuncs.com"]
  }
  EOF
  
  sudo systemctl daemon-reload
  sudo systemctl restart docker
  ```

  

