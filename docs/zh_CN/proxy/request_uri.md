#### 请求的URI

Janus使用的另外一种把请求路由到上游服务的方式为：通过`proxy.listen_path`属性指定一个请求URI。
为满足这个字段的条件，客户端请求的URI**必须**以`proxy.listen_path`字段的值开头。

比如，在一个以如下方式配置的请求中：

```json
{
    "name": "My API",
    "proxy": {
        "listen_path": "/hello/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET"],
    }
}
```
下面的请求将会匹配配置的API：

```http
GET /hello HTTP/1.1
Host: my-api.com
```

```http
GET /hello/resource?param=value HTTP/1.1
Host: my-api.com
```

```http
GET /hello/world/resource HTTP/1.1
Host: anything.com
```

对于每个请求，Janus检测到他们的URI以其中一个API的`proxy.listen_path`属性值匹配。
默认情况下，Janus会把请求原样转交到上游，**保持URI不变**。

当通过前缀代理URI时，**最长的URI最先被匹配**。这使我们可以定义两个URI： `/service` 和
`/service/resource`，确保前一个不会遮蔽后一个。
