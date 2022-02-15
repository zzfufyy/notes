#### 【1】Arrays类

---------------

* 性质

  工具类都是静态方法。

  - fill 填充

  - sort

    使用的是快速排序

    ```java
    public static void sort(int[] a) {
      DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
    }
    ```

  - binarysearch

    二分查找

  - equals

    