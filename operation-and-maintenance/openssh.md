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

在`/etc/ssh/sshd_config`中找到配置项`PermitRootLogin`，调整其值为`yes`或`no`即可。如:

```
PermitRootLogin no
```

##### 2.2 设置远程登录时的Banner

在`/etc/ssh/sshd_config`中找到配置项`Banner`，调整期值为任意文本文件即可。如:

```
Banner /etc/issue.net
```

##### 2.3 配置免密码登录

首先生成服务器端的公钥和私钥

```bash
ssh-keygen
```


检查服务端是否有`~/.ssh/authorized_keys`文件，如果没有创建一个。
复制客户端公钥到此文件即可。如:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDc/oAITBcHEVmoB9+qjsXLduucjAZ6qiROGrc7e/7tdXwM8vJjX06Frr4NrNVyb5Fm5opGjOnS7cKnz5EmqgBdS0pLptpyCH7N/ZgLRJCE6PhJGWrNg0HOp6FF4k9YLBgNEUIFoFfM90DVubta5WGehVDfF4awkIigN9Xxo2n+Wxdf0T1LIPdUh3U5IULiSgnLEmTImY9TlJbyetDscKMhNH7AzsneHv8T2Rl2nPSRtJiNrzPEbrtu7vcDDzeF1xW8lvx/kMK5MRBCGCQewLcbUp627hs4GL8CxbB1etR76UShuXTOFG0jwge5y3gnNnRnjreSVkw051u2cTCOBxXP yingzhuo@mac15.local
```

**注意：**修改配置之后需重启服务

#### 3. 参考资料

* [OpenSSH官方网站](http://www.openssh.com/)
