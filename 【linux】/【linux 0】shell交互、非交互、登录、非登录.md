#### 【linux 0】shell交互、非交互、登录、非登录

-----------------

* 简述

  可参考文章[关于“.bash_profile”和“.bashrc”区别的总结](https://blog.csdn.net/duzilonglove/article/details/79729840)

  首先，这是从两个不同维度来划分的。

  一个是是否交互，一个是否登录。

  交互 -  shell 终端交互

  非交互 - 读取的是以shell脚本

  登录 - 用户名密码 打开的shell

  非登录 - 不需要 用户名密码 打开的shell

  - 登录用户读取都是  profile

  - 交互式非登录shell  读取的是 rc， 如 ftp

* 交互式和非交互式

  - 交互式

    指在终端上执行，shell等待你的输入，并且立即执行提交的命令

    执行`$-`，可以看到默认参数

    ```bash
    $ echo $-
    himBH
    ```

    参数解释：

    - h - hashall

      打开这个选项后，Shell 会将命令所在的路径记录下来，避免每次都要查询。

    - i - interactive

      交互式shell

    - m - monitor mode

      打开监控模式

      Job control is enabled。 打开这个选项，可以控制该job到后台执行。

    - B brace expansion

      打开花括号扩展

      如：`$ cp /your/path/to/file{,.bak}`

      复制bak文件

    - H - history expand 

      记录到history中

      可以通过 history 命令查看，每一行是序号 + 执行的命令。

      在 shell 退出时，会将这些信息保存到~/.bash_history 文件中，

  - 非交互式

    读取文件的指令。

    以`shell script`方式执行。这种模式下，shell不与你进行交互，而是读取存放在文件中的命令。

    读到文件的EOF符号时，即停止输入。

    ```bash
    $ echo $-
    hB
    ```

    

* 登录和非登录

  - 登录

    需要用户名和密码，或者通过`--login` 生成的shell

    登录shell（包括tty1~tty6登录shell和使用“--login”选项的交互shell），

    它会首先读取和执行`/etc/profile`全局配置文件中的命令，

    然后依次查找

    `~/.bash_profile`

    `~/.bash_login` 

    `~/.profile`

    `logout` 退出登录

  - 非登录shell

    不需要输入用户名和密码，如命令`bash`，直接进入bash  shell。

    **如  ftp用户，软件用户等等，其作为用户无法登录**

    在非登录shell中，只读取

    **~/.bashrc （和 /etc/bash.bashrc、/etc/bashrc ）文件，**

    不同发行版本里面可能有所不同。

- `profile`与`rc`系列

  <img src="【linux 0】shell交互、非交互、登录、非登录.assets/截屏2021-03-06 上午12.09.25.png" alt="登录与非登录" style="zoom:50%;" />

  原理上讲

  交互/非交互登录shell启动时会执行加载`profile`系列的`startup`文件。

  交互式非登录shell会执行`rc`系列的`startup`文件。

  ```bash
  [root@localhost ~]# su chen
  execute ~/.bashrc
  bash-4.2$ exit
  exit
  [root@localhost ~]# 
  ```

  