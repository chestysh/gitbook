# SpringBoot安全访问

> 由于Elasticsearch开启X-PACK中的安全功能，当我们的SpringBoot应用访问Elasticsearch时，也需要设置用户名和密码了！

- 我们可以直接在SpringBoot中设置超级管理员账号，但这不是个好办法，我们还是自己建个角色和账号

- 首先在Kibana中创建一个应用访问专用的角色`app_user`；

![](/assets/elk_security_04_1644894925.png)

- 创建一个用户并配置好该角色，账号密码为`app:123456`；

![](/assets/elk_security_05_1644894961.png)

- 修改SpringBoot应用的配置文件`application.yml`，配置好账号密码即可正常访问了

```shell
spring:
  elasticsearch:
    rest:
      uris: http://localhost:9200
      username: app
      password: 123456
```
