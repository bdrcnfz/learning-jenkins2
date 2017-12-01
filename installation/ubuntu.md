# Ubuntu安装

在下载页面选择"Ubuntu/Debian":

https://pkg.jenkins.io/debian-stable/

## apt-get方式

### 安装

执行以下命令安装最新版本的jenkins：

1. 为jenkins仓库增加key

    ```bash
    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    ```

1. 修改`/etc/apt/sources.list`增加jenkins仓库

    ```bash
    deb https://pkg.jenkins.io/debian-stable binary/
    ```

1. 更新并安装

    ```bash
    sudo apt-get update
    sudo apt-get install jenkins
    ```

1. 可能的报错

	如果`apt-get update`时遇到下列错误：

    ```bash
    Reading package lists... Done
    E: The method driver /usr/lib/apt/methods/https could not be found.
    N: Is the package apt-transport-https installed?
    E: Failed to fetch https://pkg.jenkins.io/debian-stable/binary/InRelease
    E: Some index files failed to download. They have been ignored, or old ones used instead.
    ```

	请按照提示安装`apt-transport-https`

	```bash
    sudo apt-get install apt-transport-https
    ```

安装完成后Jenkins 运行于8080端口。

用PS命令可以看到一些Jenkins运行的配置信息，如JENKINS_HOME:

```bash
ps -ef |grep jenkins
jenkins   7158     1  0 07:50 ?        00:00:00 /usr/bin/daemon --name=jenkins --inherit --env=JENKINS_HOME=/var/lib/jenkins --output=/var/log/jenkins/jenkins.log --pidfile=/var/run/jenkins/jenkins.pid -- /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080 --ajp13Port=-1
jenkins   7159  7158 99 07:50 ?        00:00:24 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cach
```

## 设置

安装完成之后，用浏览器打开jenkins地址，在安装插件时，会遇到问题，报错显示：

```bash
Unable to connect to Jenkins
```

解决方案如下：

1. 添加jenkins用户到root组

	sudo usermod -a -G root jenkins

2. 让jenkins监听外部IP

	编辑文件 `/etc/default/jenkins`, 在JENKINS_ARGS中增加参数 `--httpListenAddress=0.0.0.0`

    ```bash
    JENKINS_ARGS="--webroot=/var/cache/$NAME/war --httpPort=$HTTP_PORT --httpListenAddress=0.0.0.0"
	```

3. 重启jenkins，`sudo service jenkins restart`

### 更新

用apt方式安装的jenkins可以方便的升级到最新版本：

```bash
sudo apt-get update
sudo apt-get install jenkins
```


## nginx反代

为了方便访问，避免输入8080这样的端口号，考虑使用nginx做反代。

1. 在`/etc/nginx/sites-available`目录下创建文件`jenkins.dreamfly.io`

    ```json
    server {
           listen 80;

           server_name jenkins.dreamfly.io;

           location /
           {
                  proxy_pass http://127.0.0.1:8080;
                  proxy_redirect      http://127.0.0.1:8080 $scheme://jenkins.dreamfly.io;
           }
    }
    ```

2. 在`/etc/nginx/sites-enabled`目录下创建文件`jenkins.dreamfly.io`

	```bash
    sudo ln -s ../sites-available/jenkins.dreamfly.io jenkins.dreamfly.io
    sudo service nginx restart
    ```

3. 设置`jenkins.dreamfly.io`的域名解析到目标IP地址

> 此处参考资料为[Unable to Connect to Jenkins Server (Amazon Linux AMI)](https://stackoverflow.com/questions/41055669/unable-to-connect-to-jenkins-server-amazon-linux-ami)
