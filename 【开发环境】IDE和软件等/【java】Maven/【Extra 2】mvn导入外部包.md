#### 【Extra 2】mvn导入外部包

--------------------------------------------

* 简介

  网上存在3种打入外部jar包的方法，这里只取其中最保险的：

  加入到本地仓库

* 方法

  mvn install:install-file 

  ​    -Dfile   目的jar包

  ​	-DgroupId    目的groupid

  ​	-DartifactId

  ​    -Dversion

  ​    -Dpackaging

  ```bash
  mvn install:install-file -Dfile=gbase-connector-java-8.3.81.53-build55.2.1-bin.jar -DgroupId=com.gbase -DartifactId=jdbc -Dversion=8.3.81.53 -Dpackaging=jar 
  ```

  