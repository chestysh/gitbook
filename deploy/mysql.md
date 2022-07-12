# MySQL安装

- 下载`MySQL5.7`的docker镜像：

```shell
docker pull mysql:5.7
```

- 使用如下命令启动`MySQL`服务：

```shell
docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root  \
-d mysql:5.7
```

- 参数说明

  - -p 3306:3306：将容器的3306端口映射到主机的3306端口
  - `-v /mydata/mysql/conf:/etc/mysql`：将配置文件夹挂在到主机
  -` -v /mydata/mysql/log:/var/log/mysql`：将日志文件夹挂载到主机
  - `-v /mydata/mysql/data:/var/lib/mysql/`：将数据文件夹挂载到主机
  - `-e MYSQL_ROOT_PASSWORD=root`：初始化root用户的密码

- 进入运行`MySQL`的docker容器：

```shell
docker exec -it mysql /bin/bash
```
- 使用`MySQL`命令打开客户端：

```shell
mysql -uroot -proot --default-character-set=utf8
```
- 创建mall数据库：

```shell
create database mall character set utf8
```
- 安装上传下载插件

```shell
yum -y install lrzsz
```
- 创建一个`reader:123456`帐号并修改权限，使得任何ip都能访问：

```shell
rant all privileges on *.* to 'reader' @'%' identified by '123456';
```
