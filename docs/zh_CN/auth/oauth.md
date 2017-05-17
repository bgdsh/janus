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

| 配置                 | 描述                                                                               |
|-------------------------------|-------------------------------------------------------------------------------------------|
| name                          | OAuth服务器具备唯一性的名字                                                      |
| oauth_endpoints.authorize     | Defines the [proxy configuration](/docs/config/proxy.md) for the `authorize` endpoint     |
| oauth_endpoints.token         | Defines the [proxy configuration](/docs/config/proxy.md) for the `token` endpoint         |
| oauth_endpoints.info          | Defines the [proxy configuration](/docs/config/proxy.md) for the `info` endpoint          |
| oauth_endpoints.revoke        | Defines the [proxy configuration](/docs/config/proxy.md) for the `revoke` endpoint        |
| oauth_client_endpoints.create | Defines the [proxy configuration](/docs/config/proxy.md) for the `create` client endpoint |
| oauth_client_endpoints.remove | Defines the [proxy configuration](/docs/config/proxy.md) for the `remove` client endpoint |
| allowed_access_types          | The allowed access types for this oauth server                                            |
| allowed_authorize_types       | The allowed authorize types for this oauth server                                         |
| auth_login_redirect           | The auth login redirect URL                                                               |
| secrets                       | A map of client_id: client_secret that allows you to authenticate only with the client_id |
| token_strategy.name           | The token strategy for this server. Could be `storage` or `jwt`                           |
| token_strategy.settings.secret| If you use JWT you should set your secret or private certificate string here              |
