#### `preserve_host` 属性

当进行代理时，Janus的默认行为是将请求的Host头设置为API的`upstream_url`属性的hostname。
`preserve_host`字段接收一个布尔值来告诉Janus改变这个行为。

比如，当`preserve_host`未改变时，API的配置如下：

```json
{
    "name": "My API",
    "hosts": ["service.com"],
    "proxy": {
        "listen_path": "/foo/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET"]
    }
}
```
来自客户端的请求可能会是：

```http
GET / HTTP/1.1
Host: service.com
```
Janus 将会从API的`upstream_url`字段的hostname取出Host请求头的值，然后发送如下请求到上游服务：

```http
GET / HTTP/1.1
Host: my-api.com
```

然而，当显性配置API`preserve_host=true`时：

```json
{
    "name": "My API",
    "hosts": ["example.com", "service.com"],
    "proxy": {
        "listen_path": "/foo/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET"],
        "preserve_host": true
    }
}
```

假设同样的请求从客户端发来:

```http
GET / HTTP/1.1
Host: service.com
```

Janus将保留客户端请求的Host头，然后将下面的请求发送到上游服务中：

```http
GET / HTTP/1.1
Host: service.com
```
