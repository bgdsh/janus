#### 请求的HTTP方法

客户端请求也可以通过指定`methods`字段来路由。
默认情况下，Janus将会把请求路由到API，不管它所用的HTTP方法。
但当这个字段设置了值，只有特定HTTP方法的请求会匹配。

这个字段也会接受多个值。下面的是一个允许`GET`和`HEAD`方法的API：

```json
{
    "name": "My API",
    "proxy": {
        "strip_path" : true,
        "listen_path": "/hello/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET", "HEAD"]
    }
}
```

这个API将会匹配下面的请求:

```http
GET / HTTP/1.1
Host:
```

```http
HEAD /resource HTTP/1.1
Host:
```

但不会匹配`POST`或`DELETE`请求。这使我们可以更加细粒度地配置API和中间件。
比如，可以想像两个API指向同一个上游服务的情形：一个API允许无限制地无需认证地`GET`请求，
另一个API只允许经过认证的并且有频率限制的`POST`请求（可以通过在这些请求应用验证和频率限制插件实现）。
