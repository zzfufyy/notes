### 【0】Browser对象

-----------

- Window

  - window对象属性

    - document

      只读引用

    - navigator

      返回navigator的只读引用

    - frames

      返回frame数组

    - **opener**

      返回创建此窗口的窗口的引用

      ```html
      <!DOCTYPE html>
      <html>
      <head>
      <meta charset="utf-8">
      <title>菜鸟教程(runoob.com)</title>
      <script>
      function openWin(){
          myWindow=window.open('','','width=200,height=100');
          myWindow.document.write("<p>这是我的窗口</p>");
          myWindow.focus();
          myWindow.opener.document.write("<p>这个是源窗口!</p>");
      }
      </script>
      </head>
      <body>
      
      <input type="button" value="打开我的窗口" onclick="openWin()" />
      
      </body>
      </html>
      ```

    - parent

      返回父窗口

      