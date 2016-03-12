# Gradle

#### 1. 下载
Gradle官方网站[下载](http://gradle.org/gradle-download/)二进制分发包

#### 2. 安装

解压到`/usr/local/gradle-2.11`

#### 3. 配置

```
export GRADLE_HOME=/usr/local/gradle-2.11
export PATH:$PATH:$GRADLE_HOME/bin
```

在`~/.gradle/gradle.properties`添加

```
 org.gradle.daemon=true
 org.gradle.parallel=true
```

#### 4. 测试

```bash
gradle -v
```
