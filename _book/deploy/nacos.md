# nacos 注册中心安装

- 提供好了Docker Compose脚本，直接执行即可

```shell
version: '3'
services:
  nacos-registry:
    image: nacos/nacos-server:1.3.0
    container_name: nacos-registry
    environment:
      - "MODE=standalone"
    ports:
      - 8848:8848
```

```shell
docker-compose -f docker-compose-env.yml up -d
```

- 目前已经发布2.x版本，支持长链接，可以使用自定义数据库操作

```shell
### 设置数据库类型
spring.datasource.platform=mysql

### 数据库的数量，可配置多个数据:
db.num=1

### 数据库连接信息:
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user.0=nacos_config
db.password.0=password
```

- 启动命令

```shell
 解压命令
     tar -zxvf ****.tar.gz  -C  目录
 运行命令centos
     cd nacos
     cd bin  
     sh startup.sh -m standalone
 运行命令ubuntu
     cd nacos
     cd bin
     bash startup.sh -m standalone
 运行命令win
    startup.cmd -m standalone
```

- 设置集群配置

	- 按照上述操作，配置多台（至少三台）Nacos服务后，执行如下命令创建集群配置文件：

```shell
cp /usr/local/nacos/cluster.conf.example /usr/local/nacos/cluster.conf
```

将集群节点按如下格式配置在文件中，默认8848端口可不配置

```shell
#it is ip
# example
192.168.16.101:8847
192.168.16.102
192.168.16.103
```


[官方文档地址](https://nacos.io/zh-cn/docs/2.0.0-upgrading.html "官方文档地址")
