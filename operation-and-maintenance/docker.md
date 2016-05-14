# Docker

#### 安装

```bash
curl -sSL https://get.docker.com/ | bash
sudo usermod -aG docker yingzhuo
```

#### 重启

```bash
service docker stop
service docker start
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

# Parallels Desktop bug，DNS无法解析 'https://registry-1.docker.io/'
# 添加此行， 强制使用谷歌免费DNS
# 需翻墙

echo "nameserver 8.8.8.8" > /etc/resolv.conf
/etc/init.d/docker stop  >/dev/null 2>&1
/etc/init.d/docker start >/dev/null 2>&1

exit 0
```

**Note :** 本脚本可加入 "/etc/rc.local"，这样每次开机都会重启`Docker`。
