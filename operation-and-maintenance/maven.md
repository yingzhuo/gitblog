# Maven

#### 1. 下载
在maven官方网站[下载](http://maven.apache.org/download.cgi)二进制分发版

#### 2. 安装

将`apache-maven-3.3.9.zip`解压到`/usr/local/apache-maven-3.3.9`

#### 3. 配置

```
export M2_HOME=/usr/local/apache-maven-3.3.9
export PATH=$PATH:$M2_HOME/bin
```

#### 4. 测试

```bash
mvn --version
```