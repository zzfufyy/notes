#### 【mac 0】java环境

--------------------------

* 安装环境

  从官网下载jdk8，并安装

  `java -version`

  配置`/etc/.bash_profile`

  ```bash
  JAVA_HOME=/Library/java/JavaVirtualMachines/jdk1.8.0_281.jdk/Contents/Home/
  CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
  PATH=$JAVA_HOME/bin:$PATH:
  export JAVA_HOME
  export CLASSPATH
  export PATH
  ```

  其中：

  - rt.jar

    JRE下，runtime缩写。运行时不可缺少的jar包。

     rt.jar 默认就在Root Classloader的加载路径里面的，而在Claspath配置该变量是不需要的；

    同时jre/lib目录下的

    其他jar:jce.jar、jsse.jar、charsets.jar、resources.jar都在Root Classloader中

  - tools.jar

    tools.jar 是系统用来编译一个类的时候用到的，即执行javac的时候用到

    javac XXX.java。

    实际上就是运行

    `java -Classpath=%JAVA_HOME%\lib\tools.jar xx.xxx.Main XXX.java`

    javac就是对上面命令的封装 所以tools.jar 也不用加到classpath里面

  - dt.jar

    运行环境的类库，主要是swing的包。