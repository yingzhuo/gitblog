# SpringBoot配置参考

```properties
# profile
spring.profiles.active=default

# banner
spring.main.banner-mode=off

# server
server.error.path=/error

# logging (日志文件采用logback-spring.xml配置)
#logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss.SSS,GMT+8} [%thread] %-5level %logger{72}[%L] - %msg%n
#logging.level.=info
#logging.level.com.mycompany.myproject=debug
#logging.level.org.hibernate=warn
#logging.level.org.springframework=warn

# jackson
spring.jackson.time-zone=GMT+8
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss
spring.jackson.locale=zh_CN
spring.jackson.serialization.indent_output=true
spring.jackson.serialization.fail_on_self_references=true
spring.jackson.serialization.write_dates_as_timestamps=false
spring.jackson.serialization.write_null_map_values=false
spring.jackson.serialization.write_empty_json_arrays=true
spring.jackson.serialization.write_single_elem_arrays_unwrapped=false
spring.jackson.serialization.write_enums_using_to_string=true
spring.jackson.serialization.order_map_entries_by_keys=false
spring.jackson.serialization-inclusion=always
spring.jackson.mapper.use_annotations=true
spring.jackson.mapper.sort_properties_alphabetically=false

# datasource
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://mysql_host_name:3306/database_name
spring.datasource.username=root
spring.datasource.password=root

# jpa
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.naming_strategy=org.hibernate.cfg.EJB3NamingStrategy
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
```
