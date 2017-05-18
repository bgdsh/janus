# 代理配置

| 配置                   | 描述                                                         |
|-----------------------|------------------------------------------------------------- |
| preserve_hosts        | 启用 [保留 host](/docs/proxy/preserve_host_property.md) 定义   |
| listen_path           | 定义要暴露在Janus暴露的[路径](/docs/proxy/request_uri.md)        |
| upstream_url          | 定义 OAuth 提供者的请求[路径](/docs/proxy/upstream_url.md)       |
| strip_path            | 开启代理的[清理 URI](/docs/proxy/strip_uri_property.md) 规则     |
| enable_load_balancing | 为此代理开启负载均衡                                             |
| methods               | 定义此代理支持的[methods](/docs/proxy/request_http_method.md)   |
| hosts                 | 定义此代理支持的 [hosts](/docs/proxy/request_http_header.md)    |
