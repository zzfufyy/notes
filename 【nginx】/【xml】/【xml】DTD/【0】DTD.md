#### DTD

-----------

* 前言

  DTD已经被 XML Schemas替代。

  要用到的话，看runoob教程：https://www.runoob.com/dtd/dtd-tutorial.html

  Document Type Definition

  作用是定义XLM文档的合法构建模块

  可被成行的声明在XML文档中，也可以作为一个外部引用

* 举例

  ```xml
  
  <!-- 内部声明 -->
  <?xml version="1.0"?>
  <!DOCTYPE note [
  	<!ELEMENT note (to,from,heading,body)>
  	<!ELEMENT to (#PCDATA)>
  	<!ELEMENT from (#PCDATA)>
  	<!ELEMENT heading (#PCDATA)>
  	<!ELEMENT body (#PCDATA)>
  ]>
  <!-- 外部声明 -->
  <!DOCTYPE root-element SYSTEM "filename">
  
  <note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend</body>
  </note>
  ```

* 构建模块

  xml文档构成：

  - 元素

  - 属性

  - 实体：用来定义普通文本的变量。

    实体引用是对实体的引用。如  &nbsp就是实体引用。

  - PCDATA：被解析的字符串数据，parsed character data。  <> PCDATA </>

  - CDATA: character data   不会被解析的数据

* DTD元素

  元素需要通过元素声明进行声明

  ```dtd
  <!ELEMENT element-name category>
  或
  <!ELEMENT element-name (element-content)>
  
  <!-- 空元素 使用关键词 EMPTY-->
  <!ELEMENT br EMPTY>
  
  <!-- 只含有PCDATA 的元素 -->
  <!ELEMENT element-name (#PCDATA)>
  
  <!-- 带有任何内容的元素 -->
  <!ELEMENT element-name ANY>
  
  <!-- 带有子元素的序列 -->
  <!ELEMENT element-name (child1)>
  或
  <!ELEMENT element-name (child1,child2,...)>
  
  ...
  
  <!-- 混合内容 -->
  <!ELEMENT note (#PCDATA|to|from|header|message)*>
  ```

* DTD-属性

  ```dtd
  
  <!ATTLIST element-name attribute-name attribute-type attribute-value>
  
  DTD 实例:
  
  <!ATTLIST payment type CDATA "check">
  
  XML 实例:
  
  <payment type="check" />
  ```

  