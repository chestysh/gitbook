- 安装`yum-utils`：

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

- 为yum源添加`docker`仓库位置：

```shell
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

- 安装`docker`：

```shell
yum install docker-ce
```

- 启动`docker`：

```shell
systemctl start docker
```

- 设置开机重启

```shell
systemctl enable docker.service
```

- 更新容器的重启策略

```shell
docker update --restart=always f361b7d8465
```

- 如果你的harbor服务器是http访问,那么修改registry为http

```shell
vim /etc/docker/daemon.json

{"insecure-registries":["填你的harbor服务器地址"]}

systemctl daemon-reload

systemctl restart docker
```
