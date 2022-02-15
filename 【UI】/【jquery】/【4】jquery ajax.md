### 【4】jquery ajax

----

- load

  **$(selector).load(URL,data,callback);**

  ```js
  $(document).ready(function(){
    $("button").click(function(){
      $("#div1").load("/try/ajax/demo_test.txt",function(responseTxt,statusTxt,xhr){
        if(statusTxt=="success")
          alert("外部内容加载成功!");
        if(statusTxt=="error")
          alert("Error: "+xhr.status+": "+xhr.statusText);
      });
    });
  });
  ```

- GET

  **$.get(URL,callback);**

  get请求参数是在URL中

  ```js
  $(document).ready(function(){
  	$("button").click(function(){
  		$.get("/try/ajax/demo_test.php",function(data,status){
  			alert("数据: " + data + "\n状态: " + status);
  		});
  	});
  });
  ```

- POST

  **$.post(URL,data,callback);**

  POST第二个参数，是传参的data。

  ```js
  $(document).ready(function(){
  	$("button").click(function(){
  		$.post("/try/ajax/demo_test_post.php",{
  			name:"菜鸟教程",
  			url:"http://www.runoob.com"
  		},
  		function(data,status){
  			alert("数据: \n" + data + "\n状态: " + status);
  		});
  	});
  });
  ```

  