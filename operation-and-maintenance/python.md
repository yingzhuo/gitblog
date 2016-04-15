# Python

#### 1. 安装

Python解释器已经有了，并且包含了`2.7`和`3.4`两个版本。

如果需要升级到`3.5.1`的话，可以使用以下的指令进行编译安装。

```bash
wget https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tar.xz
tar xfvJ Python-3.5.1.tar.xz
cd Python-3.5.1
./configure --prefix=/opt/python3.5
make
sudo apt-get install tk8.6-dev
sudo make install
```

```bash
sudo ln -s /opt/python3.5/bin/python3.5 /usr/local/bin/python3
sudo ln -s /opt/python3.5/bin/idle3.5 /usr/local/bin/idle3.5
```

#### 2. pip

如果没有安装需要自行安装

```bash
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install python3-pip
```

更新`pip`

```bash
su
pip install --upgrade pip
exit
```
