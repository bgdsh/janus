# 代理认证方法
当配置API时，你可以选取下面不同的认证方法：

* 基本/摘要 认证
* OAuth 2.0
* JWT

经过我们的努力，Janus的认证已经被设计得很容易建立并且完全和网关解耦。你可以通过下面几个步骤来保护你的API：

## 配置一个新的认证提供者

首先，创建一个认证提供者。使用你选定的[配置方法](config.md)来配置你的认证提供者。

## 将认证服务附加到API
把认证配置附加到配置好的API上，它便可以发挥作用。
可以简单地通过给API增加[oauth](/docs/plugins/oauth.md)插件来实现。

## 重启服务，应用配置，收工！

## 查询OAuth服务

如果想查看已经配置的所有的认证提供者，只需要执行下面的命令：

```
http -v GET localhost:8081/oauth/servers "Authorization:Bearer yourToken" "Content-Type: application/json"
```
