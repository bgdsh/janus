# OAuth 2.0


## 1. 添加你自己的OAuth服务器

API网关的主要功能便是把请求代理到不同的服务上。既然你已经通过认证，那么可以把请求发送到`/oauth/servers`上创建一个代理。

```
http -v POST localhost:8081/oauth/servers "Authorization:Bearer yourToken" "Content-Type: application/json" < examples/apis/custom_auth.json
```

## 2. 验证你的API是否已经被添加进来

你可以通过Rest API请求所有可用的API以及网关提供的所有验证方式。只需要发一个简单的请求到 `/oauth/servers`.

```bash
http -v GET localhost:8081/oauth/servers "Authorization:Bearer yourToken" "Content-Type: application/json"
```

## 3. 通过Janus来传递请求

使用下面的cURL请求来验证Janus是否可以正确地将请求传递给OAuth服务器。

这个请求是一个简单的[OAuth 2.0]() `client_credentials`流程。你可以使用任何来尝试一下。

```bash
$ http -v GET http://localhost:8080/auth/token?grant_type=client_credentials "Authorization: Basic YourBasicToken"
```

# 参考

| 配置                           | 描述                                                      |
|-------------------------------| ------------------------------------------------------------|
| name                          | OAuth服务器具备唯一性的名字                                     |
| oauth_endpoints.authorize     | 为 `authorize` 路径定义 [代理配置](/docs/config/proxy.md)      |
| oauth_endpoints.token         | 为 `token` 路径定义 [代理配置](/docs/config/proxy.md)          |
| oauth_endpoints.info          | 为 `info` 路径定义 [代理配置](/docs/config/proxy.md)           |
| oauth_endpoints.revoke        | 为 `revoke` 路径定义 [代理配置](/docs/config/proxy.md)         |
| oauth_client_endpoints.create | 为 `create` 路径定义 [代理配置](/docs/config/proxy.md)         |
| oauth_client_endpoints.remove | 为 `remove` 路径定义 [代理配置](/docs/config/proxy.md)         |
| allowed_access_types          | 认证服务器允许的访问类型                                        |
| allowed_authorize_types       | 认证服务器允许的授权类型                                        |
| auth_login_redirect           | 认证跳转地址                                                  |
| secrets                       | 一个client_id: client_secret映射，可以只提供client_id便能完成认证 |
| token_strategy.name           | 这个服务器的token模式. 可以使`storage`或`jwt`                   |
| token_strategy.settings.secret| 如果使用jwt，需要把密钥或者私有认证字符串放在这里                   |
