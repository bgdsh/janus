### 监控

`Janus` 的监控使基于 [`hellofresh/stats-go`](https://github.com/hellofresh/stats-go)库做的.
可以通入以下环境变量完成配置:

* `STATS_DSN` - 统计后端的DSN. 在没有提供环境变量、环境变量为空字符串或者没能连接到提供的`statsd`服务器的情况下，`janus` 使用 `statsd`作为后备来处理日志。
* `STATS_PREFIX` - `statsd` 指标的前缀, 比如 `janus.dev.`, `janus.staging.`, `janus.live.`。
* `STATS_IDS` - second level ID list for URLs to generalise metric names, see details in [Generalise resources by type and stripping resource ID](https://github.com/hellofresh/stats-go#generalise-resources-by-type-and-stripping-resource-id)
