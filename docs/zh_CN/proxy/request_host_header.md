### 请求的Host头

基于Host请求头来路由一个请求是最简单的代理方式，也满足HTTP的Host请求头的设计意图。
Janus通过API实体的hosts字段来实现简单的配置。

`hosts` 接收多个值, 这些值必须以数组的形式通过管理API提供。

```json
{
    "hosts": ["my-api.com", "example.com", "service.com"]
}
```

以满足API的`hosts`条件，来自客户端的请求需将其Host请求头设置为其中之一：


```http
Host: my-api.com
```

or:

```http
Host: example.com
```

or:

```http
Host: service.com
```
