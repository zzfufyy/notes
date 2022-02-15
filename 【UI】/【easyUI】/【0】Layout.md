#### 【0】Layout

--------

- Layout

  ![img](imgs/plugins_layout.png)

  5个区域：north、south、east、west、center

  demo:

  ```html
  <body class="easyui-layout">
      <div data-options="fit:true,region:'north',title:'North Title',split:true" style="height:100px;"></div>
      <div data-options="region:'south',title:'South Title',split:true" style="height:100px;"></div>
      <div data-options="region:'east',title:'East',split:true" style="width:100px;"></div>
      <div data-options="region:'west',title:'West',split:true" style="width:100px;"></div>
      <div data-options="region:'center',title:'center title'" style="padding:5px;background:#eee;"></div>
  </body>
  ```

- 布局选项

  