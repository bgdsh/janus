##### `append_path` 属性

你可能还想把`listen_path`附加到`upstream_url`上，为了达成这个目标，
使用布尔值属性`append_path`以如下方式配置API：

```json
{
    "name": "My API",
    "proxy": {
        "append_path" : true,
        "listen_path": "/service/*",
        "upstream_url": "http://my-api.com/example",
    }
}
```

通过开启这个标记来指示Janus在代理这个API时，需要**总是**包含匹配的URI前缀到上游请求的URI上。
比如，客户端发送如下请求到上面配置的API时：

```http
GET /service/path/to/resource HTTP/1.1
Host: my-api.com
```
将会使Janus发送如下请求到上游服务。

```http
GET /example/service/path/to/resource HTTP/1.1
Host: my-api.com
```
