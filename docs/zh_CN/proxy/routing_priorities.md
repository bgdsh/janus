### 路由优先级

API通过`hosts`, `listen_path`, 和 `methods`来定义匹配规则。
对于进入的请求，所有字段都需要匹配。
但是，Janus也提供了一些可伸缩性，允许几个API配置项包含相同的值。遇到这种情况，Janus会依照优先级规则行事。

规则如下 : **当评估一个请求时，Janus会首先匹配最多的规则**.

举个例子，两个API的配置如下：

```json
{
    "name": "API 1",
    "proxy": {
        "listen_path": "/",
        "upstream_url": "http://my-api.com",
        "hosts": ["example.com"]
    }
},
{
    "name": "API 2",
    "proxy": {
        "listen_path": "/",
        "upstream_url": "http://my-api.com",
        "hosts": ["example.com"],
        "methods": ["POST"]
    }
}
```

api-2 不光有 `hosts` 字段 **还** 有 `methods` 字段, 那么它会先被匹配。这样一来，就可以防止api-1遮蔽api-2

因此, 下面的请求将匹配api-1:

```http
GET / HTTP/1.1
Host: example.com
```

下面的请求将匹配 api-2:

```http
POST / HTTP/1.1
Host: example.com
```

依照这个逻辑，如果第三个API配置了`hosts`字段，`methods`字段，`listen_path`字段，它将会首先被Janus匹配。
