# SpringBoot发布war文件

首先必须修改启动类如下:

```java
// 其他import本文中省略
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(Application.class);
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(Application.class, args);
    }

}
```

在`pom.xml`中修改打包方式为`war`

```xml
<packaging>war</packaging>
```

在依赖中指定`spring-boot-starter-tomcat`为`provided`

```xml
<dependencies>
    <!-- … -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
        <scope>provided</scope>
    </dependency>
    <!-- … -->
</dependencies>
```
