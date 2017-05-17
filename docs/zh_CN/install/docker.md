# 采用Docker方式安装

可以在Quay.io的对应仓库找到如何在Docker环境下使用Janus：[janus](https://quay.io/repository/hellofresh/janus)。也有一个[Docker Compose 模板](https://github.com/hellofresh/janus/blob/master/docker-compose.yml)内置有编排和可拓展特性。
下面是一个快速示例，展示了如何把Janus容器关联到Cassandra或PostgreSQL容器：

1. **启动数据库:**
    如果你想用数据库替代基于文件系统的配置，只需要启动一个mongodb容器：

    ```bash
    $ docker run -d --name janus-database \
                  -p 27017:27017 \
                  mongo:3.0
    ```

2. **启动键值存储:**
    可以使用Redis作为键值存储，来替代内存存储。为了达成这个目的，你只需要启动一个容器：
    还需要使用`STORAGE_DNS`来设置存储路径，格式为：`memory://localhost`，如果你用的是Redis，即为`redis://janus-storage:6379`:

    ```bash
    $ docker run -d --name janus-storage \
                  -p 6379:6379 \
                  redis:3.0
    ```


3. **启动Janus:**
    启动Janus容器，如果要用数据库存储的话，连接数据库容器；设置`DATABASE_DSN`环境变量的值为连接字符串，
    形如`mongodb://janus-database:27017/janus`:
    
    ```bash
    $ docker run -d --name janus \
                  --link janus-database:janus-database \
                  --link janus-storage:janus-storage \
                  -e "DATABASE_DSN=mongodb://janus-database:27017/janus" \
                  -e "STORAGE_DNS=redis://janus-storage:6379" \
                  -p 8080:8080 \
                  -p 8443:8443 \
                  -p 8081:8081 \
                  -p 8444:8444 \
                  quay.io/hellofresh/janus
    ```

3. **检查Janus正在运行:**

    ```bash
    $ curl http://127.0.0.1:8081/
    ```

4. **开始使用Janus:**

    通过 [快速开始](/docs/getting-started/README.md) 学习如何使用Janus。
