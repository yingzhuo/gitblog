# 软件源设置

#### 镜像选择

* [网易](http://mirrors.163.com/.help/ubuntu.html)

#### 设置

```
su
cd /etc/apt
mv sources.list sources.list.backup
wget http://mirrors.163.com/.help/sources.list.trusty
mv sources.list.trusty sources.list
exit
```

```
apt-get update
apt-get upgrade
apt-get dist-upgrade
```