# Docker

#### 安装

```bash
# 通过远程脚本安装
curl -sSL https://get.daocloud.io/docker | sh

# 添加用户组使得非root用户可不通过sudo指令使用docker
sudo usermod -aG docker <username>
```

#### 重启

```bash
service docker stop
service docker start
```

#### 配置国内镜像

[DaoCloud](https://dashboard.daocloud.io/mirror)

```
echo "DOCKER_OPTS=\"\$DOCKER_OPTS --registry-mirror=http://39be60bf.m.daocloud.io\"" | sudo tee -a /etc/default/docker
sudo service docker restart
```

#### 重启脚本

```bash
#!/usr/bin/env bash
# =============================================================================
# 功能: 重启Docker Service
# 作者: 应卓
# 日期: 2016-05-15
# =============================================================================

if [[ $EUID -ne 0 ]]; then
    echo "[NG] This script must be run as root."
    exit 1
fi

/etc/init.d/docker stop  >/dev/null 2>&1
/etc/init.d/docker start >/dev/null 2>&1

exit 0
```
