#### 【GIT】git在Linux下多用户配置

------------------------------------------

*   LINUX下多用户配置

    ```shell
    # 生成 rsa rsa.pub
    ssh-keygen -t rsa -C "comment messages" -f zyw
    # 当前目录下生成
    # zyw_rsa   zyw_rsa.pub
    # 后台启动 ssh-agent
    eval  ssh-agent -s)"
    # 私钥添加至 agent 列表
    ssh-add zyw_rsa
    # 在 远程个人仓库添加公钥 zyw_rsa.pub
    # 测试
    ssh -T zywgit@github.com
    
    # clone 下目标仓库
    # 设置本地 用户名和密码
    git config --local user.name "10242306"
    git config --local user.email "zuo.yiwei@zte.com.cn"
    ```

    