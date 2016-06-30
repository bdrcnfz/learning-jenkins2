Ubuntu安装
=========

# apt-get安装

执行以下命令安装最新版本的jenkins：

    wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins

安装完成后Jenkins 运行于8080端口。

用PS命令可以看到一些Jenkins运行的配置信息，如JENKINS_HOME:

    ps -ef |grep jenkins
    jenkins   7158     1  0 07:50 ?        00:00:00 /usr/bin/daemon --name=jenkins --inherit --env=JENKINS_HOME=/var/lib/jenkins --output=/var/log/jenkins/jenkins.log --pidfile=/var/run/jenkins/jenkins.pid -- /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080 --ajp13Port=-1
    jenkins   7159  7158 99 07:50 ?        00:00:24 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/jenkins/jenkins.war --webroot=/var/cach

### 参考资料

- [Installing Jenkins on Ubuntu](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)