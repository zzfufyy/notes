【0】IO流概述

--------

* 学习目标

  - 什么是IO流，IO流分类。
  - 字节流 和 字符流
  - 处理IO流程序开发过程中的异常

* 字符流

  **只能拷贝纯文本文件**

  ```mermaid
  graph LR
  a0[字符流]
  b1[Reader]
  b2[Writer]
  
  c1[FileReader]
  c2[BufferedReader]
  
  c3[FileWriter]
  c4[BufferedWriter]
  
  a0 --> b1
  a0 --> b2
  b1 --> c1
  b1 --> c2
  b2 --> c3
  b2 --> c4
  ```

* 字节流

  ```mermaid
  graph LR
  a0[字节流]
  b1[InputStream]
  b2[OutputStream]
  c1[FileInputStream]
  c2[BufferedtInputStream]
  c3[FileOutputStream]
  c4[BufferedOutputStream]
  
  a0 --> b1
  a0 --> b2
  b1 --> c1
  b1 --> c2
  b2 --> c3
  b2 --> c4
  
  ```

  