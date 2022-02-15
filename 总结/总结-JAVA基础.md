## 总结 - Java基础

- 数据类型

​		八大基本数据类型：

​		int、short、long、float、double、byte、char、boolean

- 三大特性：

  封装、继承、多态。

  多态：父类对象可以指向子类对象，接口。

  ​            方法可以重载。

- Java内存模型

  线程 -  本地内存 - 主内存。

- JVM内存结构

  运行时数据区：

  1. 方法区，运行时常量池

     静态变量，类变量。

  2. 堆

  3. 线程

     - JVM栈

       局部变量、操作数栈、引用连接、方法返回地址。

     - 本地方法栈

     - 程序计数器

- GC机制

  1. 新生代 eden

     复制法：分为eden和survivor区，存货的留在survivor区，其中有from to。每次复制从from+eden 到to。

     eden + survivor区

  2. 老年代  old

     标记整理法：

     survivor区存活一定周期的，放在老年代

  3. 永久代 permenant

     保存JVM自己的景泰数据、类、方法等。

- GC算法

  1. 标记-清除法：

     引用计数 + 可达性分析，清理回收的对象。

     缺点：不连续内存

  2. 复制：新生代算法

     分内存为2块，存活的复制到另一部分。

     简单高效。

     空间利用率低。

  3. 标记-整理：

     标记清除后，存活对象忘一端移动，提供连续内存。

- 线程

  Runnable接口，Thread类。

  NEW RUNNABLE BLOCKED WAITING TIMED-WAITING TERMINATED

  - 对象监视器

    wait notify synchronized

- 锁

  - 乐观锁与悲观锁

    乐观锁： 并发持乐观态度，更新时上锁，如原子类

    悲观锁：一直对操作持有锁，synchronize、lock

  - 公平锁与非公平锁

    公平锁是先获取先得的，new ReetrantLock(true)

  - 独享锁和共享锁

    ReetrantReadWriteLock

    读时共享，写独享。

  - 分段锁

    ConcurrentHashMap

  - 偏向锁

    一直被一个线程访问，   多个线程访问  -  轻量级锁

    一直获取不到锁  -> 重量级锁。

- AJAX

  核心是XMLHttpreqeust

  ```js
  xmlhttp.onreadystatechange=function()
  {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
      {
          document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
      }
  }
  xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
  xmlhttp.send();
  ```

  

 



