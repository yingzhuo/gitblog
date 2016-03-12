# Java

#### 1.下载
Oracle官方网站[下载](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)

**注意：** 注意区分64位和32位版本

#### 2.安装
将下载到的`jdk-8u73-linux-x64.tar.gz`解压到`/usr/local/java_home/`

#### 3.配置

```
export JAVA_HOME=/usr/local/java_home
export JRE_HOME=$JAVA_HOME/jre
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
```

#### 4.测试

```bash
java -version
```

如果能看到jdk版本则说明安装成功了。