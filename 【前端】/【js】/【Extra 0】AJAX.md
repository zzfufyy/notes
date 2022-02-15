### AJAX

-------------

#### 1. 概念

- AJAX = Asychronous JavaScript and XML （异步的Javascript 和 XML）
- Ajax不是一种新的编程语言，而是一种用于创建web应用程序的技术。

#### 2. 原生JS实现AJAX

- XMLHttpRequest对象步骤

  | 方法                                                       | 描述                                                         |
  | ---------------------------------------------------------- | ------------------------------------------------------------ |
  | abort()                                                    | 停止当前请求                                                 |
  | getAllRequestHeaders()                                     | 把HTTP请求的所有响应首部作为键值对返回                       |
  | getResponseHeader("header")                                | 返回指定首部的串值                                           |
  | open("method","URL",[asyncFlag],["userName"],["password"]) | 建立对服务器的调用。method参数可以是GET、POST或PUT。url参数可以是相对URL或绝对URL。这个方法还包括3个可选的参数，是否异步，用户名，密码 |
  | send(content)                                              | 向服务器发送请求                                             |
  | setRequestHeader("header", "value")                        | 把指定首部设置为所提供的值。在设置任何首部之前必须先调用open()。设置header并和请求一起发送 ('post'方法一定要 ) |

- 5步创建

  1. 创建XMLHttpRequest对象

  2. 使用open方法设置和服务器的交互信息
  3. 设置发送的数据，开始和服务器交互
  4. 注册事件
  5. 更新界面

- get请求

  ```js
  //步骤一:创建异步对象
  var ajax = new XMLHttpRequest();
  //步骤二:设置请求的url参数,参数一是请求的类型,参数二是请求的url,可以带参数,动态的传递参数starName到服务端
  ajax.open('get','getStar.php?starName='+name);
  //步骤三:发送请求
  ajax.send();
  //步骤四:注册事件 onreadystatechange 状态改变就会调用
  ajax.onreadystatechange = function () {   
    if (ajax.readyState==4 &&ajax.status==200) {
      // 步骤五 如果能够进到这个判断 说明 数据 完美的回来了,并且请求的页面是存在的　　　　				   		 
      // console.log(ajax.responseText);
      //输入相应的内容  　　}
  }
  
  ```

- post请求

  ```js
  //创建异步对象  
  var xhr = new XMLHttpRequest();
  //设置请求的类型及url
  //post请求一定要添加请求头才行不然会报错
  xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
   xhr.open('post', '02.post.php' );
  //发送请求
  xhr.send('name=fox&age=18');
  xhr.onreadystatechange = function () {
      // 这步为判断服务器是否正确响应
    if (xhr.readyState == 4 && xhr.status == 200) {
      console.log(xhr.responseText);
    } 
  };
  ```

#### 3. JQuery实现AJAX

- 本质就是XMLHttpRequest，对他进行了封装：

  ```js
  1. jQuery.get(url,data,success,dataType);
  2. jQuery.post(url,data,success,dataType);
  3. jQuery.getJSON();
  4. jQuery.ajax();
  ```

- 实例

  ```html
  <html>
    <head>
    	<title>ajax</title>
      <script src="${pageContext.request.contextPath}/statics/js/jquery-3.4.1.js"></script>
    </head>
    <body>
      <script type="text/javascript">
        function a1(){
          $.ajax({
            url:"${pageContext.request.contextPath}/ajax/a1"
            data:{"name":$("txtName").val()},
            success:function (data,status){
              console.log(data);
              console.log(status);
            }
            $(“txtName”).val();
        		// 发送给服务器
        
        		// 
          })；
        }
      </script>
      用户名：
      <input type="text" id="txtName" onblur="a1()">
    </body>
    
    
  </html>
  ```

  

