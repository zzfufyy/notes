Commit镜像

-----------------

- commit命令

  docker commit 提交容器称为一个新的副本

  ````shell
  docker commit -m="提交的描述信息" -a="作者” 容器id 目标镜像名:[tag]
  ````

  Docker commit -a="zyw" -m="webapps " container_id tomcat02:1.0

  <img src="imgs/截屏2021-06-09 下午5.10.59.png" style="zoom:67%;" />

  Commit 提交获取一个镜像

如同虚拟机vm时一个快照。