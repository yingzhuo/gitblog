# OpenSSH

#### 安装OpenSSH

安装无比轻松，只需要一条命令即可。

```
sudo apt-get install openssh-server
```

安装好以后检查`ssh`服务是否成功打开

```
ps -e | grep ssh
```

如没有成功打开，需要手动将其打开

```
sudo /etc/init.d/ssh restart
```

#### 配置文件

`/etc/ssh/sshd_config`