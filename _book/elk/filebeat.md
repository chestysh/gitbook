# 安装filebeat步骤

```shell
地址：https://www.elastic.co/cn/downloads/beats/filebeat
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.3.0-linux-x86_64.tar.gz
tar zxvf filebeat-7.3.0-linux-x86_64.tar.gz
mv filebeat-7.3.0-linux-x86_64.tar.gz filebeat
```

- 启动命令

```shell
./filebeat -e -c filebeat.yml
```

- 守护进程

```shell
./filebeat -e -c filebeat.yml &
空格
exit  退出才能使守护进程起作用
```

- 不记录 filebeat 日志信息的启动方式

```shell
nohup ./filebeat -e -c /etc/filebeat/filebeat.yml > /dev/null 2>&1 &
或
nohup ./filebeat -c /etc/filebeat/filebeat.yml -e > /dev/null 2>&1 &
Ctrl+d 命令退出.
或
nohup ./filebeat -c /etc/filebeat/filebeat.yml -e &
exit 命令退出
```

- 记录filebeat 日志

```shell
./filebeat -e -c /etc/filebeat/filebeat.yml > filebeat.log &
Ctrl+d 命令退出.
```

- 停止 filebeat

```shell
ps -ef |grep filebeat 查找进程
kill -9 进程号 命令杀死进程
```

##### 配置文件

```shell
 multiline.negate: false
  multiline.match: after
  paths:
    - /data/app/mall-app/logs/spring.log/error/*.log
  fields:
    index_name: "app_log"
- type: log
  enabled: true
  #不以[开头的行都合并到上一行的末尾
  multiline.type: pattern
  multiline.pattern: '^\[
  multiline.negate: true
  multiline.match: after
  paths:
    - /data/app/mall-admin/logs/spring.log/error/*.log
  fields:
    index_name: "admin_log"
- type: log
  enabled: true
  #不以[开头的行都合并到上一行的末尾
  multiline.type: pattern
  multiline.pattern: '^[0-9]{8}'
  multiline.negate: false
  multiline.match: after
  paths:
    - /data/app/mall-search/logs/spring.log/error/*.log
  fields:
    index_name: "search_log"


# # # 7.x的版本中需要禁用此索引生命周期，否则在指定es索引名字的时候会有问题
setup.ilm.enabled: false
setup.template.name: "***-log"
setup.template.pattern: "*"
setup.template.enabled: true
setup.template.overwrite: false

# 输出到es
output.elasticsearch:
  #worker: 1
  #bulk_max_size: 1500
  hosts: ["**.**.**.**:9200"]
  index: "log-%{[fields.index_name]}-*"
  username: "elastic"
  action: "index"
  codec: json
  password: "***"
  indices:
    - index: "log-web-%{+yyyy.MM.dd}"
      when.equals:
        fields.index_name: "web_log"
```
