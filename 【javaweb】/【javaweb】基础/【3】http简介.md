#### 【3】http简介

---------

* 什么是HTTP

  超文本传输协议

  - 简单的请求响应协议，通常运行在TCP协议上
  - 指定消息交互格式。

  http的两个时代：

  - http1.0
    - HTTP/1.0：客户端与web服务器连接后只能获得一个资源，断开连接（一次性）。
  - http2.0
    - HTTP/1.1：客户端与web服务器连接后，可以获得多个web资源。

* HTTP请求

  请求行：

  - 例：

    ```txt
    Request URL: https://www.baidu.com/sugrec?prod=....
    Request Method: GET
    Status Code: 200 OK
    Remote Address: 112.80.248.75:443
    Referrer Policy: unsafe-url
    ```

  - 请求方式： GET、POST、DELETE...

    - GET:  请求携带参数较小，大小有限制，会在URL地址中显示数据内容，不安全，但高效
    - POST：请求携带的参数没有限制，大小没有限制，不会再URL地址栏显示数据内容，安全，但不高效

  请求头：

  - 例

    ```txt
    Accept: application/json, text/javascript, */*; q=0.01
    Accept-Encoding: gzip, deflate, br
    Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
    Connection: keep-alive
    Cookie:.......
    Host: www.baidu.com
    Referer: https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&ch=&tn=baiduerr&bar=&wd=mac%E6%89%93%E5%BC%80%E6%A0%B9%E7%9B%AE%E5%BD%95
    sec-ch-ua: "Google Chrome";v="89", "Chromium";v="89", ";Not A Brand";v="99"
    sec-ch-ua-mobile: ?0
    Sec-Fetch-Dest: empty
    Sec-Fetch-Mode: cors
    Sec-Fetch-Site: same-origin
    User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
    ```

    

* HTTP响应

  - 响应头
  
    ```txt
    Content-Length: 677
    Content-Type: text/plain; charset=UTF-8
    Date: Fri, 09 Apr 2021 09:43:42 GMT
    ```
  
    