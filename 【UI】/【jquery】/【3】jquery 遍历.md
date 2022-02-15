### 【3】jquery遍历

--------

- 遍历祖先
  - parent()     父元素
  - parents()   返回object  ， 祖先元素集合
  - parentsUntil()   返回介于两个给定元素之间的所有祖先元素。

- 遍历后代

  - children()
  - find()

- 水平遍历

  - siblings()    返回所有同胞元素
  - next()   下一个
  - nextAll()  所有跟随的同胞元素
  - nextUntil("h6")  返回元素之间的同胞元素
  - prev()
  - prevAll()
  - prevUntil()

- 过滤

  first()

  last() 

  eq(index)   返回指定索引元素

  filter(".blue")  返回带 class 有blue的元素

  not(".blue")  返回不带 class 有blue的元素

​		