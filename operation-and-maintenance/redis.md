# Redis

#### 安装

```bash
sudo apt-get update
sudo apt-get install redis-server
```

#### 配置

编辑`/etc/redis/redis.conf`

```
# 设置登录密码
# (取消注释) (设置密码为1234)
requirepass 1234

# 允许远程访问
#bind 127.0.0.1
```

#### 重启

```bash
sudo /etc/init.d/redis-server restart
```

#### 本地客户端

```bash
redis-cli -a 1234
```
