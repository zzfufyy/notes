### 【2】jquery HTML

-----

- jquery DOM操作

  - text() - 设置或返回所选元素的文本内容

  - html() - 设置或返回所选元素的内容（包括 HTML 标记）

  - val() - 设置或返回**表单字段**的值

    text()、html() 以及 val()，同样拥有回调函数。

    回调函数有两个参数：被选元素列表中当前元素的下标，以及原始（旧的）值。然后以函数新值返回您希望使用的字符串。

  ```js
  $("#btn1").click(function(){
      $("#test1").text(function(i,origText){
          return "旧文本: " + origText + " 新文本: Hello world! (index: " + i + ")"; 
      });
  });
  ```

  - 获取属性

    ```js
    $("button").click(function(){
      alert($("#runoob").attr("href"));
    });
    ```

    - **prop()函数的结果:**
      1. 如果有相应的属性，返回指定属性值。
      2. 如果没有相应的属性，返回值是空字符串。

    - **attr()函数的结果:**
      1. 如果有相应的属性，返回指定属性值。
      2. 如果没有相应的属性，返回值是 undefined。

    改变属性：

    ```js
    $("button").click(function(){
        $("#runoob").attr({
            "href" : "http://www.runoob.com/jquery",
            "title" : "jQuery 教程"
        });
    });
    ```

- 添加元素

  - append() - 在被选元素的结尾插入内容
  - prepend() - 在被选元素的开头插入内容
  - after() - 在被选元素之后插入内容
  - before() - 在被选元素之前插入内容

- 删除元素
  - remove() - 删除被选元素（及其子元素）
  - empty() - 从被选元素中删除子元素

- 操作css
  - addClass() - 向被选元素添加一个或多个类
  - removeClass() - 从被选元素删除一个或多个类
  - toggleClass() - 对被选元素进行添加/删除类的切换操作
  - css() - 设置或返回样式属性
- 尺寸
  - width()
  - height()
  - innerWidth()
  - innerHeight()
  - outerWidth()
  - outerHeight()