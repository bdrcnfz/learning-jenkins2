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

2. 修改`/etc/apt/sources.list`增加jenkins仓库

    ```bash
    deb https://pkg.jenkins.io/debian-stable binary/
    ```

3. 更新并安装

    ```bash
    sudo apt-get update
    sudo apt-get install jenkins
    ```

安装完成后Jenkins 运行于8080端口。

用PS命令可以看到一些Jenkins运行的配置信息，如JENKINS_HOME:

    ps -ef |grep jenkins
    jenkins   7158     1  0 07:50 ?        00:00:00 /usr/bin/daemon --name=jenkins --inherit --env=JENKINS_HOME=/var/lib/jenkins --output=/var/log/jenkins/jenkins.log --pidfile=/var/run/jenkins/jenkins.pid -- /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080 --ajp13Port=-1
    jenkins   7159  7158 99 07:50 ?        00:00:24 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cach

### 更新

用apt方式安装的jenkins可以方便的升级到最新版本：

```bash
sudo apt-get update
sudo apt-get install jenkins
```

### 参考资料

- [~~Installing Jenkins on Ubuntu~~](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)：此资料已经过期