# nohub

* 功能：后台启动进程，并不挂断运行。
* 语法：`nohub {COMMAND} &`
* 例子：

  ```
  JAVA_FILE=/var/myapp/myapp.jar
  PROFILES=default,product
  STD_LOG=/var/log/myapp.out
  ERR_LOG=/var/log/myapp.err.out

  nohup java -jar -Djava.security.egd=file:/dev/./urandom ${JAVA_FILE} --spring.profiles.active=${PROFILES} 1> ${STD_LOG} 2> ${ERR_LOG} &
  ```
