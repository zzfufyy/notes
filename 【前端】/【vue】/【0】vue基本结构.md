### 【0】vue基本结构

-------

- vue应用

  每个vue应用都需要实例化Vue实现

  ```html
  <div id="vue_det">
      <h1>site : {{site}}</h1>
      <h1>url : {{url}}</h1>
      <h1>{{details()}}</h1>
  </div>
  <script type="text/javascript">
      var vm = new Vue({
          el: '#vue_det',
          data: {
              site: "菜鸟教程",
              url: "www.runoob.com",
              alexa: "10000"
          },
          methods: {
              details: function() {
                  return  this.site + " - 学的不仅是技术，更是梦想！";
              }
          }
      })
  </script>
  ```

  - el

    选择元素

  - data

    定义属性

  - methods：

    定义函数

  - {{}}

    输出对象，函数返回值

- 附加

  除了数据属性，vue还提供了一些有用的实例属性和方法

  以$开头，区分用户定义属性。

  ```html
  <div id="vue_det">
      <h1>site : {{site}}</h1>
      <h1>url : {{url}}</h1>
      <h1>Alexa : {{alexa}}</h1>
  </div>
  <script type="text/javascript">
  // 我们的数据对象
  var data = { site: "菜鸟教程", url: "www.runoob.com", alexa: 10000}
  var vm = new Vue({
      el: '#vue_det',
      data: data
  })
   
  document.write(vm.$data === data) // true
  document.write("<br>") 
  document.write(vm.$el === document.getElementById('vue_det')) // true
  </script>
  ```

  