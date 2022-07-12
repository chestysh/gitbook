# 使用Docker Compose部署

#### 下载`Docker Compose`

```shell
curl -L https://get.daocloud.io/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

- 修改该文件的权限为可执行

```shell
chmod +x /usr/local/bin/docker-compose
```

- 查看是否已经安装成功

```shell
docker-compose --version
```

#### 使用`Docker Compose`的步骤

- 使用`Dockerfile`定义应用程序环境，一般需要修改初始镜像行为时才需要使用；
- 使用`docker-compose.yml`定义需要部署的应用程序服务，以便执行脚本一次性部署；
- 使用`docker-compose up`命令将所有应用服务一次性部署起来。

#### `Docker Compose`常用命令

- 构建、创建、启动相关容器

```shell
# -d表示在后台运行
docker-compose up -d
```

- 指定文件启动

```shell
docker-compose -f docker-compose.yml up -d
```

- 停止所有相关容器

```shell
docker-compose stop
```

- 列出所有容器信息

```shell
docker-compose ps
```

### 使用`Docker Compose `部署应用

- 编写`docker-compose.yml`文件

> Docker Compose将所管理的容器分为三层，工程、服务及容器。docker-compose.yml中定义所有服务组成了一个工程，services节点下即为服务，服务之下为容器。容器与容器直之间可以以服务名称为域名进行访问，比如在mall-tiny-docker-compose服务中可以通过jdbcmysql//db:3306这个地址来访问db这个mysql服务。

```shell
version: '3'
services:
  # 指定服务名称
  db:
    # 指定服务使用的镜像
    image: mysql:5.7
    # 指定容器名称
    container_name: mysql
    # 指定服务运行的端口
    ports:
      - 3306:3306
    # 指定容器中需要挂载的文件
    volumes:
      - /mydata/mysql/log:/var/log/mysql
      - /mydata/mysql/data:/var/lib/mysql
      - /mydata/mysql/conf:/etc/mysql
    # 指定容器的环境变量
    environment:
      - MYSQL_ROOT_PASSWORD=root
  # 指定服务名称
  mall-tiny-docker-compose:
    # 指定服务使用的镜像
    image: mall-tiny/mall-tiny-docker-compose:0.0.1-SNAPSHOT
    # 指定容器名称
    container_name: mall-tiny-docker-compose
    # 指定服务运行的端口
    ports:
      - 8080:8080
    # 指定容器中需要挂载的文件
    volumes:
      - /etc/localtime:/etc/localtime
      - /mydata/app/mall-tiny-docker-compose/logs:/var/logs
```
