# SpringBootJar启动脚本

下面的脚本名为`man.sh`用来管理名为`spring-mini`的项目

```bash
#!/usr/bin/env bash
################################################################################
# 功能: 管理spring-mini项目
# 作者: 应卓
# 日期: 2016-03-18
################################################################################

DIR=/home/yingzhuo/projects/spring-mini
JAR_FILE=$DIR/lnk.jar
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
        fi
    fi
}

function start {
    nohup java -jar -Djava.security.egd=file:/dev/./urandom ${JAR_FILE} --spring.profiles.active=${PROFILES} 1> ${STD_LOG} 2> ${ERR_LOG} &
    echo $! > $PID_FILE
    echo "[OK] Started."
}

function relink {
    target=$(find $DIR -regex '^.*-[0-9]*\.jar$' -type f | sort | tail -n 1)
    rm -rf $JAR_FILE 2> /dev/null
    ln -s $target $JAR_FILE
    echo "[OK] Relinked."
}

function autoremove {
    count=$(find $DIR -regex '^.*-[0-9]*\.jar$' | wc -l)

    if [ "$count" -gt 1 ]
    then
        find $IDR -regex '^.*-[0-9]*\.jar$' -type f | sort | sed -e '$ d' | xargs rm -rf 2>/dev/null
        echo "[OK] Autoremoved."
    fi
}

function help {
    echo "Parameter: start | stop | restart | relink | autoremove | all"
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
    relink )
        relink
        ;;
    autoremove )
        autoremove
        ;;
    all )
        stop
        relink
        start
        autoremove
        ;;
    * )
        help
esac

exit 0
```

```
yingzhuo@ubuntu:~/projects$ tree -a spring-mini/
spring-mini/
├── lnk.jar -> /home/yingzhuo/projects/spring-mini/spring-mini-20160323100133.jar
├── man.sh
├── pid
├── spring-mini-20160323100133.jar
├── spring-mini.log.err
└── spring-mini.log.std

0 directories, 6 files
```
