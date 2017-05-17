# Summary

* [简介](README.md)
* 安装
    * [Docker](install/docker.md)
* 快速开始
    * [认证](quick_start/auth.md)
    * [文件系统](quick_start/file_system.md)
    * [MongoDB](quick_start/mongodb.md)
    * [代理认证方法](quick_start/proxy_auth_methods.md)
* [代理 参考](proxy/README.md)
    * [术语](proxy/terminology.md)
    * [概览](proxy/overview.md)
    * [路由功能](proxy/routing_capabilities.md)
    * [Host请求头](proxy/request_host_header.md)
        * [使用包含通配符的主机名](proxy/wildcard_hostnames.md)
        * [`preserve_host`属性](proxy/preserve_host_property.md)
    * [请求 URI](proxy/request_uri.md)
        * [`strip_path` 属性](proxy/strip_uri_property.md)
        * [`append_path` 属性](proxy/append_uri_property.md)
    * [Request HTTP method](proxy/request_http_method.md)
    * [路由优先级](proxy/routing_priorities.md)
    * [结语](proxy/conclusion.md)
* 验证
    * [OAuth 2.0](auth/oauth.md)
* 插件
    * [OAuth](plugins/oauth.md)
    * [访问频率限制](plugins/rate_limit.md)
    * [CORS](plugins/cors.md)
* 杂项
    * [监控](misc/monitoring.md)
    * [健康检查](misc/health_checks.md)
* 升级日志
    * [2.x 到 3.x](upgrade/3x.md)
