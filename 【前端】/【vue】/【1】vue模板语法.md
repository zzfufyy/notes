### 【1】vue模板语法

---------

**vue使用了基于HTML的模板语法**

允许开发者声明式的将DOM绑定至底层Vue实例的数据。

- 插值

  {{}}

- v-html

  ```html
  <div id="app">
      <div v-html="message"></div>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: '<h1>菜鸟教程</h1>'
    }
  })
  </script>
  
  ```

- v-bind

  绑定属性，

  以下实例判断 use 的值，如果为 true 使用 class1 类的样式，否则不使用该类：

  ```html
  <div id="app">
    <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
    <br><br>
    <div v-bind:class="{'class1': use}">
      v-bind:class 指令
    </div>
  </div>
      
  <script>
  new Vue({
      el: '#app',
    data:{
        use: false
    }
  });
  </script>
  ```

- 表达式

  ```html
  <div id="app">
      {{5+5}}<br>
      {{ ok ? 'YES' : 'NO' }}<br>
      {{ message.split('').reverse().join('') }}
      <div v-bind:id="'list-' + id">菜鸟教程</div>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      ok: true,
      message: 'RUNOOB',
      id : 1
    }
  })
  </script>
  ```

- 指令

  指令是带有 v- 前缀的特殊属性。

  指令用于在表达式的值改变时，将某些行为应用到 DOM 上

  ```html
  <div id="app">
      <p v-if="seen">现在你看到我了</p>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      seen: true
    }
  })
  </script>
  ```

- 参数

  参数在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：

  ```html
  <div id="app">
      <pre><a v-bind:href="url">菜鸟教程</a></pre>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      url: 'http://www.runoob.com'
    }
  })
  </script>
  ```

  在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。

  另一个例子是 v-on 指令，它用于监听 DOM 事件：

  ```html
  <a v-on:click="doSomething">
  ```

- 修饰符

  修饰符是以半角句号 **.** 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

  例如，**.prevent** 修饰符告诉 **v-on** 指令对于触发的事件调用 **event.preventDefault()**：

  ```html
  <form v-on:submit.prevent="onSubmit"></form>
  ```

- v-model

  在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：

  ```html
  <div id="app">
      <p>{{ message }}</p>
      <input v-model="message">
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'Runoob!'
    }
  })
  </script>
  ```

  **v-model** 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，

  根据表单上的值，自动更新绑定的元素的值。

- 过滤器

  Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：

  ```html
  <!-- 在两个大括号中 -->
  {{ message | capitalize }}
  
  <!-- 在 v-bind 指令中 -->
  <div v-bind:id="rawId | formatId"></div>
  ```

  

  ```html
  <div id="app">
    {{ message | capitalize }}
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'runoob'
    },
    filters: {
      capitalize: function (value) {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1)
      }
    }
  })
  </script>
  
  ```

- 缩写

  ### v-bind 缩写

  Vue.js 为两个最为常用的指令提供了特别的缩写：

  ```
  <!-- 完整语法 -->
  <a v-bind:href="url"></a>
  <!-- 缩写 -->
  <a :href="url"></a>
  ```

  ### v-on 缩写

  ```
  <!-- 完整语法 -->
  <a v-on:click="doSomething"></a>
  <!-- 缩写 -->
  <a @click="doSomething"></a>
  ```