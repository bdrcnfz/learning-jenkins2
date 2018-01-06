# 重置密码

如果不小心忘记了jenkins的账户密码，则可以通过下列方式重置：

```bash
cd /var/lib/jenkins
sudo vi config.xml
```

修改`userSecurity`为`false`：

```xml
<userSecurity>false</userSecurity>
```

删除`<authorizationStrategy>`和`<securityRealm>`两段内容。

然后重新启动jenkins

```bash
sudo sudo service jenkins restart
```

