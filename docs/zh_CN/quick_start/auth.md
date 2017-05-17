# Janus中的认证
开始使用Janus提供的管理API之前，需要获得一个[JSON Web Token](https://jwt.io)，并且在每个请求中都附带`Authorization`这个请求头。

你需要执行下面的命令来获取一个token:

```sh
http -v --json POST localhost:8081/login username=admin password=admin
```
用户名和密码定义在叫做`web.credentials.username`和`web.credentials.password`的配置项中。默认是*admin*/*admin*。

<p align="center">
  <a href="http://g.recordit.co/dDjkyDKobL.gif">
    <img src="http://g.recordit.co/dDjkyDKobL.gif">
  </a>
</p>

你可以使用这个token来请求Janus的管理API。
