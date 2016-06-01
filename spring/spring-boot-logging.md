# SpringBoot记录日志

SpringBoot默认使用 slf4j + logback 记录日志

#### 我常用的配置

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

#### 通过profiles细化logback配置

可添加`classpath:/logback-spring.xml`

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<logback>
    <springProfile name="staging">
    <!-- configuration to be enabled when the "staging" profile is active -->
    </springProfile>

    <springProfile name="dev, staging">
        <!-- configuration to be enabled when the "dev" OR "staging" profiles are active -->
    </springProfile>

    <springProfile name="!production">
        <!-- configuration to be enabled when the "production" profile is NOT active -->
    </springProfile>
</logback>
```
