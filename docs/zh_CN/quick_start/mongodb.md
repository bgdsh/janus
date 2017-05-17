# 添加你自己的API - MongoDB版本

如果选用了MongoDB, 那么所有的配置都可以通过REST API完成。因为所有的API都是被保护的，所以我们需要[登录](auth.md)。

## 1. 添加API

API网关的主要功能便是把请求代理到不同的服务上。通过验证之后，便可以发一个请求到`/apis`上来创建一个代理。

```
http -v POST localhost:8081/apis "Authorization:Bearer yourToken" "Content-Type: application/json" < examples/apis/posts.json
```

<p align="center">
  <a href="http://g.recordit.co/Hi7SX8s5IA.gif">
    <img src="http://g.recordit.co/Hi7SX8s5IA.gif">
  </a>
</p>

当请求`GET /posts`时，会被代理到`https://jsonplaceholder.typicode.com/posts`。

## 2. 验证API是否已经成功添加

你可以使用REST API来查询所有可用的API和验证方案。只需向`/apis`发送一个请求即可：

```bash
http -v GET localhost:8081/apis "Authorization:Bearer 你的token" "Content-Type: application/json"
```

## 3. 通过Janus传递请求

使用下面的cURL来验证Janus是否可以正确地把请求传递到你的API。需要注意一下，默认情况下，Janus在端口`:8080`处理代理请求：

```bash
$ http -v GET http://localhost:8080/posts/1
```

<p align="center">
  <a href="http://g.recordit.co/vufeMjwEfg.gif">
    <img src="http://g.recordit.co/vufeMjwEfg.gif">
  </a>
</p>

如果响应成功，则表明Janas已经把发到`http://localhost:8080`的请求代理到第1步设置的`upstream_url`上，
然后请求结果会被传递给我们。

想保护你的API吗?  查看 [这个文档](proxy_auth_methods.md) 里的方法。
