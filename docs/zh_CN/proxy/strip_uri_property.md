##### `strip_path` 属性

可能会需要指定一个URI前缀来匹配一个API，但是不想把它包含在上游请求中。
为达到这个目的，使用`strip_path`这个布尔值属性以如下方式配置：

```json
{
    "name": "My API",
    "proxy": {
        "strip_path" : true,
        "listen_path": "/service/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET"]
    }
}
```

开启这个标记表明当Janus代理这个API时，在上游请求URI中，**不**应该包含配配的URI前缀。
比如，下面的客户端发送请求到上面配置API：

```http
GET /service/path/to/resource HTTP/1.1
Host: my-api.com
```

Janus将会发送下面的请求到上游服务：

```http
GET /path/to/resource HTTP/1.1
Host: my-api.com
```
