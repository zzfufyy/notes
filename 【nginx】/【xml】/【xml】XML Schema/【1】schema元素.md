#### schema元素

------

* \<schema>元素

  是每一个XML Schema的 **根元素**

  举例：

  ```xml
  <?xml version="1.0"?>
  
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://www.runoob.com"
  xmlns="http://www.runoob.com"
  elementFormDefault="qualified">
  ...
  ...
  </xs:schema>
  ```

  - Xmlns 指定元素、和数据类型来自于命名空间   http://www.w3.org/2001/XMLSchema

    **使用其元素和数据类型需要加上    前缀  xs**

  - `targetNamespace="http://www.runoob.com"`

    表示被此   schema定义的元素来自命名空间   http://www.runoob.com

  - `elementFormDefault="qualified"`

    表示任何XML实例文档所使用的的且在此schema声明过得元素必须被namespace限定

* 理解

* ```
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  ```

  您就可以使用 schemaLocation 属性了。此属性有两个值。第一个值是需要使用的命名空间。第二个值是供命名空间使用的 XML schema 的位置：

  ```
  xsi:schemaLocation="http://www.runoob.com note.xsd"
  ```

  这个 xmlns:xsi 在不同的 xml 文档中似乎都会出现。
  
   这是因为， xsi 已经成为了一个业界默认的用于 XSD(（XML Schema Definition) 文件的命名空间。
  
  ```
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"
  ```
  
  上面这行的语法其实是：
  
  ```
  xsi:schemaLocation = "键" "值"
  ```
  
  这个 xmlns:xsi 在不同的 xml 文档中似乎都会出现。
  
  这是因为， xsi 已经成为了一个业界默认的用于 XSD(（XML Schema Definition) 文件的命名空间。
  
  ```
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"
  ```
  
  上面这行的语法其实是：
  
  ```
  xsi:schemaLocation = "键" "值"
  ```
  
  即 xsi 命名空间下 schemaLocation 元素的值为一个由空格分开的键值对。
  
  前一个"键" http://maven.apache.org/POM/4.0.0 指代 【命名空间】， 只是一个全局唯一字符串而已。
  
  后一个值指代 【XSD location URI】 , 这个值指示了前一个命名空间所对应的 XSD 文件的位置， 
  
  xml parser 可以利用这个信息获取到 XSD 文件， 
  
  从而通过 XSD 文件对所有属于 命名空间 http://maven.apache.org/POM/4.0.0 的元素结构进行校验， 
  
  因此这个值必然是可以访问的， 且访问到的内容是一个 XSD 文件的内容。

