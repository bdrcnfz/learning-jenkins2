CentOS 6.5 安装
==============

# yum安装

执行yum命令:

	yum install jenkins

安装完成之后, 通过ps命令可以看到jenkins的进程, 还可以看到其他一些信息:


    [root@localhost ~]# ps -ef | grep jenkins
    jenkins    976     1  6 11:25 ?        00:00:33 /usr/bin/java -Dcom.sun.akuma.Daemon=daemonized -Djava.awt.headless=true -DJENKINS_HOME=/var/lib/jenkins -jar /usr/lib/jenkins/jenkins.war --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war --daemon --httpPort=8080 --debug=5 --handlerCountMax=100 --handlerCountMaxIdle=20


可以通过 `service jenkins start/stop` 命令来控制jenkins:

    [root@localhost ~]# service jenkins stop
    Shutting down Jenkins                                      [  OK  ]
    [root@localhost ~]# service jenkins start
    Starting Jenkins                                           [  OK  ]
