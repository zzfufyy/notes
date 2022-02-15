【0】Junit4简介

------------------------

* 简介

  单元测试框架

  - 提供 注释 识别测试方法

  - 提供 断言 测试预期结果

* 注解

  | 注解          | 描述                                                         |
  | ------------- | ------------------------------------------------------------ |
  | @Test         | 测试注解，标记一个方法可以作为一个测试用例 。                |
  | @Before       | 测试类的每个方法之前执行。                                   |
  | @BeforeClass  | 前置静态方法。如数据库连接。                                 |
  | @After        | 测试类的每个方法之后执行。                                   |
  | @AfterClass   | 清理资源等事后工作。                                         |
  | @Ignore       | 暂时忽略                                                     |
  | @Runwith      | @Runwith就是放在测试类名之前，用来确定这个类怎么运行的。也可以不标注，会使用默认运行器。 |
  | @Parameters   | 用于使用参数化功能。                                         |
  | @SuiteClasses | 用于套件测试                                                 |
  
* 断言

  | 断言                                                         | 描述                                                         |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | void assertEquals([String message],expected value,actual value) | 断言两个值相等。值类型可能是int，short，long，byte，char，Object，第一个参数是一个可选字符串消息 |
  | void assertTrue([String message],boolean condition)          | 断言一个条件为真                                             |
  | void assertFalse([String message],boolean condition)         | 断言一个条件为假                                             |
  | void assertNotNull([String message],java.lang.Object object) | 断言一个对象不为空（null）                                   |
  | void assertNull([String message],java.lang.Object object)    | 断言一个对象为空（null）                                     |
  | void assertSame([String message],java.lang.Object expected,java.lang.Object actual) | 断言两个对象引用相同的对象                                   |
  | void assertNotSame([String message],java.lang.Object unexpected,java.lang.Object actual) | 断言两个对象不是引用同一个对象                               |
  | void assertArrayEquals([String message],expectedArray,resultArray) | 断言预期数组和结果数组相等，数组类型可能是int，short，long，byte，char，Object |

* 执行过程

  ```java
  public class JunitTest {
  
      @BeforeClass
      public static void beforeClass() {
          System.out.println("in before class");
      }
  
      @AfterClass
      public static void afterClass() {
          System.out.println("in after class");
      }
  
      @Before
      public void before() {
          System.out.println("in before");
      }
  
      @After
      public void after() {
          System.out.println("in after");
      }
  
      @Test
      public void testCase1() {
          System.out.println("in test case 1");
      }
  
      @Test
      public void testCase2() {
          System.out.println("in test case 2");
      }
  
  }
  ```

  

* 断言实例

  ```java
  public class AssertionTest {
  
      @Test
      public void test() {
          String obj1 = "junit";
          String obj2 = "junit";
          String obj3 = "test";
          String obj4 = "test";
          String obj5 = null;
          
          int var1 = 1;
          int var2 = 2;
  
          int[] array1 = {1, 2, 3};
          int[] array2 = {1, 2, 3};
  
          Assert.assertEquals(obj1, obj2);
  
          Assert.assertSame(obj3, obj4);
          Assert.assertNotSame(obj2, obj4);
          
          Assert.assertNotNull(obj1);
          Assert.assertNull(obj5);
  
          Assert.assertTrue(var1 < var2);
          Assert.assertFalse(var1 > var2);
  
          Assert.assertArrayEquals(array1, array2);
  
      }
  }
  // 结果
  in before class
  in before
  in test case 1
  in after
  in before
  in test case 2
  in after
  in after class
  ```

* 时间测试

  ```java
  @Test(timeout = 1000)
  public void testCase1() throws InterruptedException {
      TimeUnit.SECONDS.sleep(5000);
      System.out.println("in test case 1");
  }
  ```

* 异常测试

  ```java
  @Test(expected = ArithmeticException.class)
  public void testCase3() {
      System.out.println("in test case 3");
      int a = 0;
      int b = 1 / a;
  }
  ```

  