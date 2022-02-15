#### 【linux 1】bashrc和bash_profile

----------------

* bash的stratup文件

  - `/etc/profile`

    系统初始化文件，在`login shells`执行

  - `/etc/bash.bash_logout`

    系统的登陆shell清理，当一个登陆shell退出时执行

  - `~/.bash_profile`

    个人初始化文件，为登录shell文件。

  - `~/.bashrc`

    每个交互式shell启动文件

  - `~/bash_logout`

    单个登录shell清理文件，当一个登录shell退出时执行

* `profile`与`rc`系列

  其位于不同的运行场景，**即根据shell的运行模式不同**

  **bash有登录和交互**两种模式，

  