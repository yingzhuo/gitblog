# tomcat

#### 1. 下载

[官网地址](http://tomcat.apache.org/download-80.cgi)

#### 2. 安装

将下载的目录解压，软连接至`/usr/local/tomcat`

#### 3. 配置

在`/usr/local/tomcat/bin/startup.sh`中添加

```bash
# Better OS/400 detection: see Bugzilla 31132
os400=false
case "`uname`" in
OS400*) os400=true;;
esac

# 以下内容为添加
JAVA_HOME=/usr/local/java8
JRE_HOME=/usr/local/java8/jre
PATH=$JAVA_HOME/bin:$JRE_HOME:$PATH
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
TOMCAT_HOME=/usr/local/tomcat
JAVA_OPTS=$JAVA_OPTS
```

添加一条环境变量

```
export JAVA_OPTS="-Xms256m -Xmx512m -Djava.security.egd=file:/dev/./urandom"
```

如需Tomcat在开机时自动启动

`/etc/rc.local`中添加

```bash
/usr/local/tomcat/bin/startup.sh
```

#### 4. 重启

```bash
/usr/local/tomcat/bin/shutdown.sh
/usr/local/tomcat/bin/startup.sh
```
