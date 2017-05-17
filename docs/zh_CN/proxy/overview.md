
### 概览

从一个比较高的视角上看，Janus将从代理端口（可配置，默认`8080`）上监听请求，
判别当前请求对应的上游服务，为该API运行配置好的中间件，然后将请求转交给上游的API或者服务。

当客户端发送的请求到达代理端口，Janus会判别把进入的请求路由（或者转交）给哪个上游服务或者API。
判别是基于Janus中的配置。配置使通过管理API管理的。可以通过多个属性来配置API，但3个相关属性为主机、地址和方法。

如果Janus无法判定将当前的请求路由到哪个上游API，Janus会响应：

```http
HTTP/1.1 404 Not Found
Content-Type: application/json
Server: Janus/<x.x.x>

{
    "message": "no API found with those values"
}
```
