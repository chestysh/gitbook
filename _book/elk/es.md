# Elasticsearch设置密码

- 修改Elasticsearch的配置文件并开启`X-PACK`中的安全功能，该配置文件在安装目录的`config`文件夹下面，例如`elasticsearch-7.6.2\config\elasticsearch.yml`；

```shell
http.cors.enabled: true
http.cors.allow-origin: "*"
http.cors.allow-headers: Authorization
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
```

- 启动Elasticsearch服务

- 在`bin`目录下使用如下命令`elasticsearch-setup-passwords interactive`修改预置账号的密码，期间需要设置多个账号密码，我都设置成了123456；


![](/assets/elk_security_01_1644894045.png)

- 期间设置了好几个账号

```shell
elastic：超级管理员账号
kibana：Kibana访问专用账号
logstash_system：Logstash访问专用账号
beats_system：FileBeat访问专用账号
apm_system：APM系统专用账号
remote_monitoring_user：远程监控账号
```

- 接下来我们需要在Kibana的配置文件中添加可以访问`Elasticsearch`的账号，该配置文件在安装目录的config文件夹下面，例如`kibana-7.6.2\config\kibana.yml`；

```shell
elasticsearch.username: "kibana"
elasticsearch.password: "123456"
```

- 启动Kibana服务

- 当`Kibana`启动完成后，我们访问的时就需要登录认证了，使用超级管理员账号`elastic:123456`可以进行登录，访问地址：http://localhost:5601

![](/assets/elk_security_02_1644894189.png)

- 登录成功后，在我们的`Management`选项中可以找到安全相关的配置，在此我们可以对用户、角色、权限进行设置。

![](/assets/elk_security_03_1644894332.png)
