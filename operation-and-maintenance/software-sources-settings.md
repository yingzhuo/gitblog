# 软件源设置

#### 镜像选择

* [网易](http://mirrors.163.com/.help/ubuntu.html)

#### 设置

```
su
cd /etc/apt
mv sources.list sources.list.ori
wget http://mirrors.163.com/.help/sources.list.trusty
mv sources.list.trusty sources.list
exit
```

```
apt-get update
apt-get upgrade
apt-get dist-upgrade
```

#### 备份

14.04 (trusty)

* 163

```
deb http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
```

* alibaba (trusty)

```
deb http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe

```

#### 更新软件源脚本

```bash
#!/usr/bin/env bash
# =============================================================================
# 功能: 设置apt源
# 作者: 应卓
# 日期: 2016-04-14
# =============================================================================

if [[ $EUID -ne 0 ]]; then
    echo "[NG] This script must be run as root."
    exit 1
fi

CODENAME=$(lsb_release -a 2>/dev/null | tail -1 | awk '{print $2}')

echo "\
deb http://mirrors.aliyun.com/ubuntu/ $CODENAME main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ $CODENAME-backports main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ $CODENAME-proposed main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ $CODENAME-security main multiverse restricted universe
deb http://mirrors.aliyun.com/ubuntu/ $CODENAME-updates main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ $CODENAME main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ $CODENAME-backports main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ $CODENAME-proposed main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ $CODENAME-security main multiverse restricted universe
deb-src http://mirrors.aliyun.com/ubuntu/ $CODENAME-updates main multiverse restricted universe" > /etc/apt/sources.list

exit 0
```
