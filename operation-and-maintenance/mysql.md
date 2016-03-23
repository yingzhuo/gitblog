# MySQL

#### 安装

```bash
sudo apt-get update
sudo apt-get install mysql-server
```

#### 设置字符集

编辑`/etc/mysql/my.cnf`

```
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init-connect='SET NAMES utf8mb4'

# bind-address = 127.0.0.1 #这一行要注释掉
```

#### 开启远程登录

使用mysql客户端以`root`身份登录并执行

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

#### 重启

```bash
sudo /etc/init.d/mysql restart
```
