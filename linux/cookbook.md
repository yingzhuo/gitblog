# Shell Cookbook

#### 判断当前用户是否为`root`用户

```bash
if [[ $EUID -ne 0 ]]; then
    echo "[NG] This script must be run as root." 1>&2
    exit 1
else
    # do something here.
    exit 0
fi
```

#### Jar文件如何作为系统服务运行

必须要一个包装器如下:

```bash
#!/bin/sh

SERVICE_NAME=spring-mini
PATH_TO_JAR=/home/yingzhuo/spring-mini/spring-mini.jar
PID_PATH_NAME=/home/yingzhuo/spring-mini/spring-mini.pid
STD_LOG=/home/yingzhuo/spring-mini/spring-mini.std.log
ERR_LOG=/home/yingzhuo/spring-mini/spring-mini.err.log

case $1 in
    start)
        echo "Starting $SERVICE_NAME ..."
        if [ ! -f $PID_PATH_NAME ]; then
            nohup java -jar -Djava.security.egd=file:/dev/./urandom $PATH_TO_JAR 1> $STD_LOG 2> $ERR_LOG &
            echo $! > $PID_PATH_NAME
            echo "$SERVICE_NAME started ..."
        else
            echo "$SERVICE_NAME is already running ..."
        fi
    ;;
    stop)
        if [ -f $PID_PATH_NAME ]; then
            PID=$(cat $PID_PATH_NAME);
            echo "$SERVICE_NAME stoping ..."
            kill $PID;
            echo "$SERVICE_NAME stopped ..."
            rm $PID_PATH_NAME
        else
            echo "$SERVICE_NAME is not running ..."
        fi
    ;;
    restart)
        if [ -f $PID_PATH_NAME ]; then
            PID=$(cat $PID_PATH_NAME);
            echo "$SERVICE_NAME stopping ...";
            kill $PID;
            echo "$SERVICE_NAME stopped ...";
            rm $PID_PATH_NAME
            echo "$SERVICE_NAME starting ..."
            nohup java -jar -Djava.security.egd=file:/dev/./urandom $PATH_TO_JAR  1> $STD_LOG 2> $ERR_LOG &
            echo $! > $PID_PATH_NAME
            echo "$SERVICE_NAME started ..."
        else
            echo "$SERVICE_NAME is not running ..."
        fi
    ;;
esac
```

把此脚本放入`/etc/init.d`即可 使用 `sudo /etc/init.d/spring-mini start`开启。<br>
`update-rc.d spring-mini defaults`叫如开机启动。
