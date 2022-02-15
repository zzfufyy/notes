### 【1】jquery效果

--------

- 隐藏显示

  hide()、show()

  ```js
  $("#hide").click(function(){
    $("p").hide();
  });
  ```

​		toggle() 切换显示隐藏。

- 淡入淡出

  fadeIn()、fadeOut()、fadeToggle()、fadeTo()

- 滑动

  slideDown()  slideUp() slideToggle()

  ```js
  $(document).ready(function(){
    $("#flip").click(function(){
      $("#panel").slideDown("slow");
    });
  });
  ```

- 动画

  $(*selector*).animate({*params*}*,speed,callback*);

  ```js
  $("button").click(function(){
    $("div").animate({
      left:'250px',
      height:'+=150px',
      width:'+=150px'
    });
  });
  ```

  停止动画：

  ```js
  $("#stop").click(function(){
    $("#panel").stop();
  });
  ```

- jquery方法链

  ```js
  $(document).ready(function()
    {
    $("button").click(function(){
      $("#p1").css("color","red").slideUp(2000).slideDown(2000);
    });
  });
  ```

  逐条执行。