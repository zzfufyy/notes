#### 【Extra 0】jadEclipse安装

-------------------------------

*原文参考：https://blog.csdn.net/chinaxiaofeng8/article/details/81773729?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.add_param_isCf&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.add_param_isCf*

**工具/原料**

- jadClipse version:3.3.0的jar包
- Eclipse Java EE IDE for Web Developers. Version: Indigo Service Release 1
- jad.exe可执行文件

**方法/步骤**

1. 先下载jadClipse的jar包

链接：sourceforge.net/projects/jadclipse/

1. 然后，将net.sf.jadclipse_3.3.0.jar拷贝到eclipse的plugins目录下；
2. 再删除eclipse的configuration目录下org.eclipse.update文件，
3. 如果，你的eclipse是开着的，点击菜单栏中File->Restart。
4. 接着，从 http://varaneckas.com/jad/ 这个链接处，下载jad的可执行文件，解压后放在某一磁盘中。
5. 设置jad的可执行文件路径以及生成的临时文件路径。
6. 设置*.class文件类型的默认打开方式