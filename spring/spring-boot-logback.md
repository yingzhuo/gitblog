# SpringBoot配置logback

#### 0. 杂项技巧

我的常用配置:

```properties
logging.pattern.console=%clr(%d{yyyy-MM-dd HH:mm:ss.SSS,GMT+8} [%thread] %-5level %logger{72}[%L] - %msg%n)
logging.level.root=warn
logging.level.com.github.yingzhuo.cheliangbao=trace
logging.level.org.springframework=warn
logging.level.org.hibernate=warn
```

可以指定日志输出的颜色

```properties
%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){yellow}
```

被支持的颜色有: <br>

`blue`
`cyan`
`faint`
`green`
`magenta`
`red`
`yellow`

#### 1. `logback-spring.xml` 可以细化配置`profile`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="false">

    <property resource="logback-spring.properties"/>

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS,GMT+8} [%thread] %-5level %logger{72}[%L] - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="DEBUG_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_DIR}/${DEBUG_LOG_FILE_NAME}.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_DIR}/${DEBUG_LOG_FILE_NAME}.%d{yyyy-MM-dd}.log.gz</fileNamePattern>
            <maxHistory>365</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS,GMT+8} [%thread] %-5level %logger{72}[%L] - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="BUSINESS_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_DIR}/${BUSINESS_LOG_FILE_NAME}.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_DIR}/${BUSINESS_LOG_FILE_NAME}.%d{yyyy-MM-dd}.log.gz</fileNamePattern>
            <maxHistory>365</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS,GMT+8}|%level|%logger|%msg%n</pattern>
        </encoder>
    </appender>

    <!--
        开发环境
    -->
    <springProfile name="dev">
        <logger name="com.github.yingzhuo.cheliangbao" additivity="false" level="DEBUG">
            <appender-ref ref="STDOUT"/>
        </logger>

        <logger name="org.springframework" additivity="false" level="WARN">
            <appender-ref ref="STDOUT"/>
        </logger>

        <logger name="org.springframework.boot" additivity="false" level="WARN">
            <appender-ref ref="STDOUT"/>
        </logger>
    </springProfile>

    <!--
        业务日志
    -->
    <springProfile name="business_log">
        <logger name="CHELIANGBAO_REST" additivity="false" level="DEBUG">
            <appender-ref ref="BUSINESS_FILE"/>
        </logger>

        <logger name="org.hibernate.SQL" additivity="false" level="DEBUG">
            <appender-ref ref="BUSINESS_FILE"/>
        </logger>
        <logger name="org.hibernate.type.descriptor.sql.BasicBinder" additivity="false" level="TRACE">
            <appender-ref ref="BUSINESS_FILE"/>
        </logger>
    </springProfile>

    <!--
        调试日志
    -->
    <springProfile name="debug_log">
        <logger name="com.github.yingzhuo.cheliangbao" additivity="false" level="DEBUG">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>

        <logger name="org.springframework" additivity="false" level="WARN">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>

        <logger name="org.springframework.boot" additivity="false" level="WARN">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>

        <logger name="CHELIANGBAO_REST" additivity="false" level="DEBUG">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>

        <logger name="org.hibernate.SQL" additivity="false" level="DEBUG">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>
        <logger name="org.hibernate.type.descriptor.sql.BasicBinder" additivity="false" level="TRACE">
            <appender-ref ref="DEBUG_FILE"/>
        </logger>
    </springProfile>

    <root level="OFF" />

</configuration>
```

#### 2. `logback-spring.properties`提供变量定义，指定日志文件位置等信息

```properties
##
# 日志存放目录
##
LOG_DIR=/tmp/logs/cheliangbao-rest/

##
# 业务日志文件名
##
BUSINESS_LOG_FILE_NAME=business

##
# 调试日志文件名
##
DEBUG_LOG_FILE_NAME=debug
```
