# Java 环境(Linux)

- 官网下载jdk,[官网](https://www.oracle.com/java/technologies/downloads/#java8 "官网")选择下载匹配的版本，如下所示

![](/assets/Feige图片20220530163506_1653899727.png)

- 下载完成后通过 xftp 上传到服务器，执行如下操作（vim 后按 i 开始编辑，esc关闭编辑，输入:wq保存关闭）：

```shell
vim /etc/profile
最下面加入这段：
#java
export JAVA_HOME=/usr/local/java/jdk1.8.0_261
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
执行这句：
mkdir -p /usr/local/java &&  tar -xzvf jdk-8u261-linux-x64.tar.gz && mv jdk1.8.0_261 /usr/local/java && source /etc/profile
```

- 验证是否安装成功 `java -version`：
