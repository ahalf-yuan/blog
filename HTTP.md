# HTTP
一个正常的 HTTP 请求

```xml
<method> <request-url> <version>
<headers>
<entity-body>
```

##### POST 方法常用的四种 MIME 类型
> []()

1. `application/x-www-form-urlencoded`   

HTML 中 <form> 标签如果不带 enctype 属性，默认就会用这种数据类型提交表单，将数据以key1=value1&key2=value2 的形式进行编码，HTTP 报文大概是下面这样子：
```
POST /api/user HTTP/1.1

Content-Type: application/x-www-form-urlencoded

name=ldj&age=16
```

2. `application/json`  
```
POST /api/user HTTP/1.1

Content-Type: application/json;charset=utf-8

{"name":"makeco", "age": 22}
```

3.`multipart/form-data`  
使用表单上传文件时，需要在 <form> 标签上设置 enctype 的值为 multipart/form-data，可以使用 FormData API 来控制表单数据，这种类型的 HTTP 报文就有点复杂：  
```
POST /api/user HTTP/1.1

Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA


------WebKitFormBoundaryrGKCBY7qhFd3TrwA

Content-Disposition: form-data; name="name"

makeco

------WebKitFormBoundaryrGKCBY7qhFd3TrwA

Content-Disposition: form-data; name="avatar"; filename="chrome.png"

Content-Type: image/png

PNG ... content of chrome.png ...

------WebKitFormBoundaryrGKCBY7qhFd3TrwA--
```

4. `text/xml`  
```
POST /user/api HTTP/1.1

Content-Type: text/xml

<?xml version="1.0"?>

<user>

 <name>makeco</name>

 <age><22/age>

</user>
```