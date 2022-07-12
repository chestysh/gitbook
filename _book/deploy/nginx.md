# Nginx安装

- 下载`Nginx1.10`的`docker`镜像：

```shell
docker pull nginx:1.10
```

- 先运行一次容器（为了拷贝配置文件）：

```shell
docker run -p 80:80 --name nginx \
-v /mydata/nginx/html:/usr/share/nginx/html \
-v /mydata/nginx/logs:/var/log/nginx  \
-d nginx:1.10
```

- 将容器内的配置文件拷贝到指定目录：

```shell
docker container cp nginx:/etc/nginx /mydata/nginx/
```

- 修改文件名称：

```shell
mv nginx conf
```

- 终止并删除容器：

```shell
docker stop nginx
docker rm nginx
```

- 使用如下命令启动Nginx服务：

```shell
docker run -p 80:80 --name nginx \
-v /mydata/nginx/html:/usr/share/nginx/html \
-v /mydata/nginx/logs:/var/log/nginx  \
-v /mydata/nginx/conf:/etc/nginx \
-d nginx:1.10
```
