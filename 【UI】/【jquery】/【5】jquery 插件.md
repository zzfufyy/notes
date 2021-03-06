### 【5】jquery 插件

------

- Validate

  | 序号 | 规则               | 描述                                                         |
  | :--- | :----------------- | :----------------------------------------------------------- |
  | 1    | required:true      | 必须输入的字段。                                             |
  | 2    | remote:"check.php" | 使用 ajax 方法调用 check.php 验证输入值。                    |
  | 3    | email:true         | 必须输入正确格式的电子邮件。                                 |
  | 4    | url:true           | 必须输入正确格式的网址。                                     |
  | 5    | date:true          | 必须输入正确格式的日期。日期校验 ie6 出错，慎用。            |
  | 6    | dateISO:true       | 必须输入正确格式的日期（ISO），例如：2009-06-23，1998/01/22。只验证格式，不验证有效性。 |
  | 7    | number:true        | 必须输入合法的数字（负数，小数）。                           |
  | 8    | digits:true        | 必须输入整数。                                               |
  | 9    | creditcard:        | 必须输入合法的信用卡号。                                     |
  | 10   | equalTo:"#field"   | 输入值必须和 #field 相同。                                   |
  | 11   | accept:            | 输入拥有合法后缀名的字符串（上传文件的后缀）。               |
  | 12   | maxlength:5        | 输入长度最多是 5 的字符串（汉字算一个字符）。                |
  | 13   | minlength:10       | 输入长度最小是 10 的字符串（汉字算一个字符）。               |
  | 14   | rangelength:[5,10] | 输入长度必须介于 5 和 10 之间的字符串（汉字算一个字符）。    |
  | 15   | range:[5,10]       | 输入值必须介于 5 和 10 之间。                                |
  | 16   | max:5              | 输入值不能大于 5。                                           |
  | 17   | min:10             | 输入值不能小于 10。                                          |

  ```js
   $("#signupForm").validate({
     rules: {
       firstname: "required",
       lastname: "required",
       username: {
         required: true,
         minlength: 2
       }
     })
  ```

- Cookie

  ```js
  $.cookie('name', 'value');
  $.cookie(); // 读取所有cookie
  $.removeCookie('name'); // => true
  ```

- Accordion

  折叠菜单

- Autocomplete

  根据用户输入值进行搜索和过滤。

- Growl

  消息提醒

- 