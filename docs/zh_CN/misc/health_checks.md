### 健康检查

可以为每一个API增加健康检查，只需设置如下属性：

*URL*: 要检查的URL

可以通过管理端API的`/status`路径来检查所有应用的健康状况。响应如下：

```
[
  {
    "name": "configurations",
    "check": {
      "status": "healthy",
      "subject": "fully operating"
    }
  },
  {
    "name": "example",
    "check": {
      "status": "partially_healthy",
      "subject": "rabbitMQ connection is not respoding"
    }
  },
  {
    "name": "foo",
    "check": {
      "status": "unhealthy",
      "subject": "postgres database down"
    }
  }
]
```

每个服务都需提供一个路径，以便Janus可以检查服务的运行状态。
路径返回的状态码会定义服务是*健康*, *部分健康* 还是 *不健康* 状态。

| 状态码           | 描述                      |
|----------------|---------------------------|
| 200 - 399      | 服务状态完好                |
| 400 - 499      | 服务部分完好                |
| 500 >          | 服务已经停止                |
