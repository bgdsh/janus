# 添加你的API - 文件系统
如果选择基于文件系统的配置方式，将会是静态的（和Nginx类似）。

## 1. 准备文件夹结构
默认情况下，所有的API配置都会被分到单独个文件中（每个API一个文件），这些文件存在于`/etc/janus`中。
当然你也可以通过赋值给`database.dsn`来配置路由，比如你可以将它的值改为`file:///usr/local/janus`。

现在用默认的文件夹 `/etc/janus`. 创建两个主要的文件夹 `apis` 和 `auth`，每个文件夹包含一组代理配置。
运行命令:

```bash
mkdir -p /etc/janus/apis
mkdir -p /etc/janus/auth
```

## 2. 添加你的API

API网关的主要功能便是将请求代理到不同的服务。那么操作如下。

只需把[这个例子](../../../examples/apis/posts.json)放入 `apis` 文件夹。
那么，当你访问`GET /posts`时，请求会自动代理到`https://jsonplaceholder.typicode.com/posts`上。

重启Janus来应用更新。

```bash
sudo sv restart janus
```

## 3. 检查API是否已经被添加上

可以通过REST API 来查询所有的API和验证方式。只需发请求到`/apis`。

```bash
http -v GET localhost:8081/apis "Authorization:Bearer yourToken" "Content-Type: application/json"
```

## 4. 通过Janus请求API

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
