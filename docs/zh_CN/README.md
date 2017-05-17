<p align="center">
  <a href="https://hellofresh.com">
    <img width="120" src="https://www.hellofresh.de/images/hellofresh/press/HelloFresh_Logo.png">
  </a>
</p>

# 雅努斯 （Janus）

[![Build Status](https://travis-ci.org/hellofresh/janus.svg?branch=master)](https://travis-ci.org/hellofresh/janus)
[![GoDoc](https://godoc.org/github.com/hellofresh/janus?status.svg)](https://godoc.org/github.com/hellofresh/janus)
[![Go Report Card](https://goreportcard.com/badge/github.com/hellofresh/janus)](https://goreportcard.com/report/github.com/hellofresh/janus)

> 一个用Go写的API网关

这是一个轻量级的API网关，也包含一个管理平台。利用它，你可以控制API的访问，包括谁可以访问、在什么时间开放访问、如何访问。
API网关也会给出详细的分析，包括用户是如何与API交互的以及错误信息。

## 为啥叫雅努斯?

> 在古罗马神话中，雅努斯是开端之神，门神，转换之神，时间之神，通途之神，终端之神。
他通常被描述为有一前一后两张脸，可以看到未来，也可以看到过去。[维基百科](https://zh.wikipedia.org/wiki/Janus)

我们认为以门神的名字给这个项目命名非常合适。

## 什么是API网关?

API网关处于你应用、服务的最前端，管理服务的验证、访问控制、流量限制，任务非常繁重。
理想状态下，你可以只关注于创建服务，而不是花精力在基础的管理平台上。
举个例子，如果你已经写了一个很棒的服务，这个服务用于提供纽约所有猫的地理位置，并且你想公开它。
那么，相对于自己写一个授权验证的中间件，把它集成到一个API网关上便是一种更快捷、更安全的方式。

## 主要功能亮点

这个API网关将提供给你强大并且轻量级的特性，助你管好自己的API生态系统。

* 远离依赖地狱：只有一个用go写的字节文件
* 支持HTTP/2
* 支持Rest API：完全的可编程访问控制，使API用户/密钥/API配置的管理变得简单。
* 访问频率控制，简单地控制用户的访问频次，粒度细化，可以精确到密钥级别。
* 跨域过滤：支持API跨域共享控制，可精确到特定的端。
* 多种认证协议：开箱即用，支持JWT、OAuth 2.0 和基本的认证方式
* 优雅地断开http连接
* 包含小型[官方](https://quay.io/repository/hellofresh/janus) docker镜像

## 安装

### Docker

安装Janus最简单的方式便是运行它的docker镜像。查看[docker-compose.yml](../ci/assets/docker-compose.yml)文件，然后运行命令。

```sh
docker-compose up -d
```

现在你可以获得来自网关的响应了。

运行下列命令:

```sh
http http://localhost:8080/
```

### 手动

你也可以现在编译后的程序然后在本地环境运行（或者是部署到你想要的地方）。
到 [发布](https://github.com/hellofresh/janus/releases) 页面下载对应的最新版.

## 开始使用

现在你已经把 *janus* 运行起来了，可以把第一个代理建立起来了. 以下两项任选:

* [文件系统](docs/quick_start/file_system.md)
* [MongoDB](docs/quick_start/mongodb.md)

## 贡献代码

开始贡献代码之前, 请查看 [贡献须知](../CONTRIBUTING.md).

## 文档

* Janus文档: https://godoc.org/github.com/hellofresh/janus
* Go语言: https://golang.org/
