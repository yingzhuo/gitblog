# OpenSSH

#### 1. 安装OpenSSH

安装无比轻松，只需要一条命令即可。

```
sudo apt-get install openssh-server
```

安装好以后检查`ssh`服务是否成功打开

```
ps -e | grep ssh
```

如没有成功打开，需要手动将其打开

以下是常用命令: (在su环境下执行)

```bash
/etc/init.d/ssh status
/etc/init.d/ssh restart
/etc/init.d/ssh start
/etc/init.d/ssh stop
```

#### 2. 配置

##### 2.1 允许/禁止`root`账户登录

在`/etc/ssh/sshd_config`中找到配置项`PermitRootLogin`，调整其值为`yes`或`no`即可。

##### 2.2 设置远程登录时的Banner

在`/etc/ssh/sshd_config`中找到配置项`Banner`，调整期值为任意文本文件即可。如:

```
Banner /etc/issue.net
```

**注意：**修改配置之后需重启服务