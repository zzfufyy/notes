#### 【extra 0】Lamda表达式

---------------

- 概念

  jdk8新增特性。

  避免内部类定义过多。

  **函数式接口**：

  - 任何接口，**如果只包含唯一一个抽象方法，**那么他就是一个函数式接口。
  - 可以用lamda表达式创建该接口的对象。
  - lamda表达式只能有一行代码才能简化成一行
  - 如果有多行，用代码块包裹。

- 实例 -- Runnable

  ```java
  new Thread(()->{
    System.out.println("test lambda");
  }).start();
  
  Runnable target = () -> {
    System.out.println("test lambda2");
  };
  new Thread(target).start();
  
  ```
  
  