# 我的gradle配置参考

### `settings.gradle`

```groovy
rootProject.name = 'parent-project'
include 'sub-project-one'
include 'sub-project-two'
```

### `build.gradle` （parent）

```groovy
buildscript {
    repositories {
        mavenLocal()
        mavenCentral()
        maven { url 'http://repo.spring.io/plugins-release' }
    }
    dependencies {
        classpath 'org.springframework.build.gradle:propdeps-plugin:0.0.7'
        classpath 'org.jetbrains.kotlin:kotlin-gradle-plugin:1.0.1'
        classpath 'org.springframework.boot:spring-boot-gradle-plugin:1.3.3.RELEASE'
    }
}

ext {
}

allprojects {
    group 'com.github.yingzhuo'
    version '1.0.0-SNAPSHOT'

    gradle.projectsEvaluated {
        tasks.withType(JavaCompile) {
            options.compilerArgs << '-Xlint:unchecked'
            options.compilerArgs << '-Xlint:deprecation'
        }
    }
}

subprojects {
    apply plugin: 'java'
    apply plugin: 'groovy'
    apply plugin: 'idea'
    apply plugin: 'maven'
    apply plugin: 'propdeps'
    apply plugin: 'propdeps-maven'
    apply plugin: 'propdeps-idea'
    apply plugin: 'propdeps-eclipse'
    apply plugin: 'spring-boot'

    sourceCompatibility = 1.8
    targetCompatibility = 1.8

    sourceSets {
        main {
            java { srcDirs = [] }
            groovy { srcDirs = ['src/main/java', 'src/main/groovy'] }
        }
    }

    compileJava.dependsOn(processResources)

    repositories {
        mavenLocal()
        mavenCentral()
    }

    dependencies {
        optional 'org.codehaus.groovy:groovy-all:2.4.6'
        optional 'org.springframework.boot:spring-boot-configuration-processor:1.3.3.RELEASE'
    }

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
}
```

### `build.gradle` (sub)

```groovy
dependencies {
    compile project(':sub-project-two')

    testCompile 'junit:junit:4.11'
}
```
