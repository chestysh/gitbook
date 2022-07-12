# Redis安装

- 下载Redis5.0的docker镜像：

```shell
docker pull redis:5
```

- 使用如下命令启动Redis服务：

```shell
docker run -p 6379:6379 --name redis \
-v /mydata/redis/data:/data \
-d redis:5 redis-server --appendonly yes
```

- 进入Redis容器使用redis-cli命令进行连接：

```shell
docker exec -it redis redis-cli
```

![](/assets/mall_linux_deploy_01_1642746912.png)
