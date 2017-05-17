### 术语

`API`: 这个术语是指Janus的API实体。你可以通过管理API来把API指向上游服务。

`中间件（Middleware）`是指Janus的『中间件』，是指代理生命周期中的执行的一些代码。中间件可以通过管理API配置。既可以在全局生效，也可以针对某个API生效。

`客户端（Client）`: 是指对Janus的代理端口发送请求的下游客户端。

`上游服务（Upstream service）`: 是指坐落于Janus之后的你自己的你自己的API/服务。