【1】File类

-----------

- 构造方法

  File(string pathName);

  File(String parent, String child);

  File(File parent, String child);

- 成员方法

  createNewFile()

  mkdir()   mkdirs()

  isDirectory()

  isFile()

  exists()

  getAbsolutePath()

  getPath()

  list() // 返回名称数组（String）

  listFiles() // 返回File类型数组

- 实践

  ```java
  package com.zyw.io;
  
  import java.io.File;
  import java.io.IOException;
  
  public class FileTest {
      public static void main(String[] args) {
          File file = new File("D:\\abc\\1.txt");
          File file2 = new File("D:\\abc","1.txt");
          File file3 = new File("D:\\abc");
          file3 = new File(file3,"1.txt");
  
          // 创建文件
          try {
              file3.createNewFile();
          } catch (IOException e) {
              e.printStackTrace();
          }
  
          // d盘下创建文件夹
          File file5 = new File("D:\\a");
          boolean flag = file5.mkdir();
          File file6 = new File("D:\\a\\b\\c");
          file6.mkdirs(); // 也可以创建单机目录
      }
  }
  
  ```

  