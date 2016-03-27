# 常用依赖

```groovy
dependencies {
    // tool
    optional 'org.springframework.boot:spring-boot-configuration-processor:1.3.3.RELEASE'

    // groovy
    compile 'org.codehaus.groovy:groovy-all:2.4.6'

    // kotlin
    testCompile 'org.jetbrains.kotlin:kotlin-test:1.0.1'
    compile 'org.jetbrains.kotlin:kotlin-runtime:1.0.1'
    compile 'org.jetbrains.kotlin:kotlin-stdlib:1.0.1'
    compile 'org.jetbrains.kotlin:kotlin-reflect:1.0.1'

    // spring-boot
    testCompile 'org.springframework.boot:spring-boot-starter-test:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-autoconfigure:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-actuator:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-aop:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-web:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-logging:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-tomcat:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-validation:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-data-jpa:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-mail:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-freemarker:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-groovy-templates:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-velocity:1.3.3.RELEASE'
    compile 'org.springframework.boot:spring-boot-starter-cache:1.3.3.RELEASE'

    // spring
    testCompile 'org.springframework:spring-test:4.2.5.RELEASE'
    compile 'org.springframework:spring-core:4.2.5.RELEASE'
    compile 'org.springframework:spring-context:4.2.5.RELEASE'
    compile 'org.springframework:spring-context-support:4.2.5.RELEASE'
    compile 'org.springframework:spring-beans:4.2.5.RELEASE'
    compile 'org.springframework:spring-aop:4.2.5.RELEASE'
    compile 'org.springframework:spring-aspects:4.2.5.RELEASE'
    compile 'org.springframework:spring-expression:4.2.5.RELEASE'
    compile 'org.springframework:spring-jdbc:4.2.5.RELEASE'
    compile 'org.springframework:spring-orm:4.2.5.RELEASE'
    compile 'org.springframework:spring-tx:4.2.5.RELEASE'
    compile 'org.springframework:spring-web:4.2.5.RELEASE'
    compile 'org.springframework:spring-webmvc:4.2.5.RELEASE'
    compile 'org.springframework:spring-oxm:4.2.5.RELEASE'
    compile 'org.springframework:spring-jms:4.2.5.RELEASE'

    // shiro
    compile 'org.apache.shiro:shiro-core:1.2.4'
    compile 'org.apache.shiro:shiro-web:1.2.4'
    compile 'org.apache.shiro:shiro-ehcache:1.2.4'
    compile 'org.apache.shiro:shiro-spring:1.2.4'

    // hibernate-validator
    compile 'org.hibernate:hibernate-validator:5.2.4.Final'

    // jetbrick-template
    compile 'com.github.subchen:jetbrick-commons:2.1.1'
    compile 'com.github.subchen:jetbrick-template:2.1.1'
    compile 'com.github.subchen:jetbrick-template-web:2.1.1'
    compile 'com.github.subchen:jetbrick-template-springmvc:2.1.1'
    compile 'org.antlr:antlr4-runtime:4.5.1'

    // jdbc
    compile 'mysql:mysql-connector-java:5.1.38'

    // dbcp
    compile 'com.zaxxer:HikariCP:2.4.3'

    // slf4j
    compile 'org.slf4j:slf4j-api:1.7.16'
    compile 'org.slf4j:jcl-over-slf4j:1.7.16'
    compile 'org.slf4j:jul-to-slf4j:1.7.16'
    compile 'org.slf4j:log4j-over-slf4j:1.7.16'
    // compile 'org.slf4j:slf4j-simple:1.7.16'

    // logback
    compile 'ch.qos.logback:logback-core:1.1.5'
    compile 'ch.qos.logback:logback-classic:1.1.5'

    // servlet-api
    compile 'javax.servlet:javax.servlet-api:3.1.0'

    // webjars
    compile 'org.webjars:jquery:2.2.0'
    compile 'org.webjars:bootstrap:3.3.6'

    // common-tools
    compile 'com.google.guava:guava:19.0'
    compile 'org.apache.commons:commons-lang3:3.4'
    compile 'org.apache.commons:commons-collections4:4.1'
    compile 'commons-io:commons-io:2.4'
    compile 'commons-net:commons-net:3.1'
    compile 'commons-logging:commons-logging:1.2'
    compile 'commons-codec:commons-codec:1.10'
    compile 'commons-beanutils:commons-beanutils:1.9.2'
    compile 'commons-fileupload:commons-fileupload:1.3.1'

    // joda-time
    compile 'joda-time:joda-time:2.9.1'
    compile 'org.jadira.usertype:usertype.spi:5.0.0.GA'
    compile ('org.jadira.usertype:usertype.core:5.0.0.GA') {
        exclude 'group': 'org.hibernate'
    }
}
```
