
### 路由的功能

现在讨论Janus如何把一个请求映射到已经配置好的主机、地址、方法等属性（或字段）。
记住，这三个字段都是可选的，但至少需要指定其中一个。
对于一个与某个API匹配的请求:

* 请求需包含所有的配置字段
* 请求中字段的值必须包含于配置的取值范围内，即配置接受一个或多个值，请求只需匹配其中一个值。


来看几个例子。 API代理配置如下:

```json
{
    "name": "My API",
    "hosts": ["example.com", "service.com"],
    "proxy": {
        "listen_path": "/foo/*",
        "upstream_url": "http://my-api.com",
        "methods": ["GET"]
    }
}
```

下面几个API会与这个配置相匹配:

```http
GET /foo HTTP/1.1
Host: example.com
```

```http
GET /foo HTTP/1.1
Host: service.com
```

```http
GET /foo/hello/world HTTP/1.1
Host: example.com
```

上面三个请求都满足了API定义中设置的条件。

然而， 下面的请求不会满足配置的条件：

```http
GET / HTTP/1.1
Host: example.com
```

```http
POST /bar HTTP/1.1
Host: example.com
```

```http
GET /foo HTTP/1.1
Host: foo.com
```

上面这个三个请求都只能满足两个配置项。第一个请求的URI和配置中所有的uri都不匹配，第二个问题出在方法上，第三个问题出在header的Host参数上。

现在我们明白了主机、地址、方法属性是如何协同工作的，接下来分别探索每一个属性。