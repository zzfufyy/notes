### nginx概念

-------------

#### 1. 介绍

- 为什么需要nginx

  <img src="imgs/截屏2021-08-14 下午3.48.50.png" alt="截屏2021-08-14 下午3.48.50" style="zoom:67%;" />

  - 中间件
  - 代理服务器
  - 负载均衡
  - 反向代理

- 什么是Nginx

  - 一个高性能的HTTP和反向代理的web服务器

  - 特点是：

    - 内存占用少

    - 并发能力强

- 正向代理和反向代理

  - 正向代理

    **代理客户端**

    - 典型例：vpn

      <img src="imgs/截屏2021-08-14 下午3.52.50.png" alt="截屏2021-08-14 下午3.52.50" style="zoom:67%;" />

  - 反向代理

    **代理服务器**

    - 典型例：访问百度等网站

      <img src="imgs/截屏2021-08-14 下午3.54.46.png" alt="截屏2021-08-14 下午3.54.46" style="zoom:67%;" />

- Ngnix负载均衡实现
  - 加权轮询
  - ip Hash（session保证在一个服务器上，但一般不用，使用redis）
  - 动静分离（静态资源，动态资源分离）

---------

#### 2. nginx命令

- 常用命令

  ```bash
  nginx     # 启动
  nginx -s stop # 停止
  nginx -s quit # 安全退出
  nginx -s reload # 重新加载配置文件
  ```

-------

#### 3. nginx配置

- 基本配置说明

  ```properties
  ## 全局配置
  # access_log logs/access.log main;
  sendfile on;
  # tcp_nopush on;
  keepalive_timeout 65;
  # gzip on;
  # http
  events{
  	worker_connectinos 1024;
  }
  ## 负载均衡配置
  upstream xxx{
  	# 服务器资源
  	server 127.0.0.1:8080 weight=1
  	server 127.0.0.1:8081 weight=1
  	
  }
  ## http配置
  http{
  	server{
  		listen      80;
  		server_name localhost;
  		# 代理 根请求
  		location / {
  			# xxxx
  			root html;
  			index index.html index.htm
  			proxy_pass http://kuangstudy;
  		}
  		# 代理其他请求
  		location /admin {
  			# xxx
  		}
  	}
  	server{
  		listen      443;
  		server_name localhost;
  	}
  }
  
  
  
  
  ```
  


