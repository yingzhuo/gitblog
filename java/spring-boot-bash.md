# SpringBoot Jar启动脚本

下面的脚本，以名为`spring-mini`的项目为例。

```bash
#!/usr/bin/env bash
################################################################################
# 功能: 管理spring-boot's jar文件的启动或停止等
# 作者: 应卓
# 日期: 2016-03-18
################################################################################

DIR=/home/yingzhuo/projects/spring-mini
JAR_FILE=$DIR/spring-mini.jar
PID_FILE=$DIR/pid
STD_LOG=$DIR/spring-mini.log.std
ERR_LOG=$DIR/spring-mini.log.err
PROFILES=default,prod

function stop {
    if [[ -f $PID_FILE ]]; then
        PID=$(cat $PID_FILE)
        kill $PID 1>/dev/null 2>&1

        if [ $? -eq 0 ]; then
            echo "[OK] Stopped."
        else
            echo "[NG] Cannot stop."
        fi
    fi
}

function start {
    nohup java -jar -Djava.security.egd=file:/dev/./urandom ${JAR_FILE} --spring.profiles.active=${PROFILES} 1> ${STD_LOG} 2> ${ERR_LOG} &
    echo $! > $PID_FILE
    echo "[OK] Started."
}

function help {
    echo "[NG] Parameter: start | stop | restart"
}

case $1 in
    stop )
        stop
        ;;
    start )
        start
        ;;
    restart )
        stop
        start
        ;;
    * )
        help
esac

exit 0
```
