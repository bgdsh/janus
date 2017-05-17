#### 使用通配符主机名

为提供可伸缩性，Janus提供了在hosts字段的主机名中加入通配符的功能。
通配符主机名认为任何匹配的Host头都满足条件，然后匹配对应的API。

通配符主机名必须只能包含一个星号，而且星号要么在域名的最左边，要么在最右边。举个例子：

`*.example.org` 将允许诸如 `a.example.com` 和 `x.y.example.com` 的Host属性匹配。
`example.*` 将允许诸如 `example.com` 和 `example.org` 的Host属性匹配。

下面是一个完整的例子：

```json
{
    "name": "My API",
    "hosts": ["*.example.com", "service.com"]
}
```

将会允许下面的请求匹配这个 API:

```http
GET / HTTP/1.1
Host: an.example.com
```

```http
GET / HTTP/1.1
Host: service.com
```
