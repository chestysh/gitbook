# RabbitMQ安装

- 下载`rabbitmq3.7.15`的`docker`镜像：

```shell
docker pull rabbitmq:3.7.15
```

- 使用如下命令启动RabbitMQ服务：

```shell
docker run -p 5672:5672 -p 15672:15672 --name rabbitmq \
-d rabbitmq:3.7.15
```

- 进入容器并开启管理功能：

```shell
docker exec -it rabbitmq /bin/bash
rabbitmq-plugins enable rabbitmq_management
```


![](/assets/mall_linux_deploy_02_1643091104.png)

- 开启防火墙：

```shell
firewall-cmd --zone=public --add-port=15672/tcp --permanent
firewall-cmd --reload
```

- 访问地址查看是否安装成功：http://192.168.3.101:15672


![](/assets/mall_linux_deploy_03_1643091173.png)

- 输入账号密码并登录：`guest guest`

- 创建帐号并设置其角色为管理员：`mall mall`


![](/assets/mall_linux_deploy_04_1643091245.png)

- 创建一个新的虚拟host为：`/mall`


![](/assets/mall_linux_deploy_05_1643091292.png)

- 点击mall用户进入用户配置页面


![](/assets/mall_linux_deploy_06_1643091335.png)

- 给`mall`用户配置该虚拟`host`的权限


![](/assets/mall_linux_deploy_07_1643091383.png)

- 命令行批量删除

```shell
关闭应用的命令为： rabbitmqctl stop_app
清除的命令为： rabbitmqctl reset
重新启动命令为： rabbitmqctl start_app
ps
查看所有队列命令： rabbitmqctl list_queues
```
