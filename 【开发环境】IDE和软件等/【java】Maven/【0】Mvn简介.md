

#### 【0】Mvn教程

-----------------------------

* 简介

  Apache下开源项目 - 项目管理工具

  基于项目对象模型（POM， Project Object Model）

* 帮助开发者完成：

  构建、文档生成、报告、依赖、SCMs、发布、分发、邮件列表

* **共同标准目录**

  | 目录                               | 目的                                                         |
  | :--------------------------------- | :----------------------------------------------------------- |
  | ${basedir}                         | 存放pom.xml和所有的子目录                                    |
  | ${basedir}/src/main/java           | 项目的java源代码                                             |
  | ${basedir}/src/main/resources      | 项目的资源，比如说property文件，springmvc.xml                |
  | ${basedir}/src/test/java           | 项目的测试类，比如说Junit代码                                |
  | ${basedir}/src/test/resources      | 测试用的资源                                                 |
  | ${basedir}/src/main/webapp/WEB-INF | web应用文件目录，web项目的信息，比如存放web.xml、本地图片、jsp视图页面 |
  | ${basedir}/target                  | 打包输出目录                                                 |
  | ${basedir}/target/classes          | 编译输出目录                                                 |
  | ${basedir}/target/test-classes     | 测试编译输出目录                                             |
  | Test.java                          | Maven只会自动运行符合该命名规则的测试类                      |
  | ~/.m2/repository                   | Maven默认的本地仓库目录位置                                  |
  
* Maven基本操作

	| 命令              | 功能                                     |
	| ----------------- | ---------------------------------------- |
	| mvn package       | 构建项目                                 |
	| mvn  clean        | 清理项目                                 |
	| mvn test          | 测试                                     |
	| mvn install       | 打包和部署到本地资源库                   |
	| mvn site          | 生成信息文档站点                         |
	| mvn site-deploy   | 通过WebDAV部署自动生成的文档站点到服务器 |
	| mvn tomcat:deploy | 以WAR方式部署到tomcat                    |



* package、install、deploy区别

  - mvn clean package依次执行了clean、resources、compile、testResources、testCompile、test、jar(打包)等７个阶段。
- mvn clean install依次执行了clean、resources、compile、testResources、testCompile、test、jar(打包)、install等8个阶段。
  - mvn clean deploy依次执行了clean、resources、compile、testResources、testCompile、test、jar(打包)、install、deploy等９个阶段。
    由上面的分析可知主要区别如下，
  - install .... 把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库
  - package命令完成了项目编译、单元测试、打包功能，但没有把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库和远程maven私服仓库
  - deploy ... 布署到本地maven仓库和远程maven私服仓库

