# Gradle Cook Book

仓库
---

#### 如何使用本地maven仓库？

`build.gradle`中添加

```
repositories {
    mavenLocal()
    mavenCentral()
}
```

#### 如何排除传递依赖？

例子: `build.gradle`中添加

```
compile ('org.springframework.boot:spring-boot-starter-groovy-templates:1.3.3.RELEASE') {
    exclude module: 'groovy'
    exclude module: 'groovy-templates'
    exclude module: 'groovy-xml'
}
```

#### gradle没有optional依赖，应该怎么办？

例子: `build.gradle`中添加

```
buildscript {
    repositories {
        mavenLocal()
        mavenCentral()
    }
    dependencies {
        classpath 'org.springframework.build.gradle:propdeps-plugin:0.0.7'
    }
}

configure(allprojects) {
    apply plugin: 'propdeps'
    apply plugin: 'propdeps-maven'
    apply plugin: 'propdeps-idea'
    apply plugin: 'propdeps-eclipse'
}
```

如此，就可以使用`optional`、`provided`形式的依赖了。

```
dependencies {
    testCompile 'junit:junit:4.11'
    provided 'org.slf4j:slf4j-api:1.7.13'
    optional 'org.springframework.boot:spring-boot-configuration-processor:1.3.3.RELEASE'
}
```

编译
---

#### 如何设置编译参数？

`build.gradle`中添加

```
gradle.projectsEvaluated {
    tasks.withType(JavaCompile) {
        options.compilerArgs << '-Xlint:unchecked'
        options.compilerArgs << '-Xlint:deprecation'
    }
}
```

#### 如何设置Java编译的版本？

`build.gradle`中添加

```
sourceCompatibility = 1.8
targetCompatibility = 1.8
```

#### 如何设置编译使用的字符集？

`build.gradle`中添加

```
compileJava.options.encoding = 'UTF-8'
```

#### 如何混合编译Java与Groovy？

`build.gradle`中添加

```
apply plugin: 'groovy'

sourceSets {
    main {
        java { srcDirs = [] }
        groovy { srcDirs = ['src/main/java', 'src/main/groovy'] }
    }
}

dependencies {
    compile 'org.codehaus.groovy:groovy-all:2.4.5'
}
```

执行
---

#### 如何执行Java的main方法

`build.gradle`中添加

```
task runHelloWorld(type: JavaExec, dependsOn: 'classes') {
    main = 'com.github.yingzhuo.gradle.example.HelloWorld'
    classpath = sourceSets.main.runtimeClasspath
    args 'we are command line arguments'
    systemProperty ('sys.prop.key', 'sys.prop.value')
}
```

发布
---

#### 我在发布时想同时发布source和docs，我应该怎么做？

`build.gradle`中添加

```
task sourcesJar(type: Jar, dependsOn: 'classes') {
    classifier = 'sources'
    from sourceSets.main.allSource
}

task javadocJar(type: Jar, dependsOn: 'javadoc') {
    classifier = 'javadoc'
    from javadoc['destinationDir']
}

artifacts {
    archives sourcesJar
    archives javadocJar
}
```

SpringBoot
---

#### 如何指定mainClass？

`build.gradle`中添加

```
springBoot {
    mainClass = 'com.mycompany.myapp.pkg.Application'
}
```
