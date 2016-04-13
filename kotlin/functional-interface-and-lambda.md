# Lambda表达式与FunctionalInterface

在`Kotlin`语言中，使用`Lambda`表达式是司空见惯的，为了与`Java8`的FunctionalInterface兼容。
今天特意进行了测试。

##### 1. 在`Kotlin`中创建`Java8`中定义的FunctionalInterface的实例

```kotlin
val consumer: Consumer<String> = Consumer {
    println(it)
}
```
上面Consumer可以想象成一个工厂方法。

##### 2. 在`Kotlin`中创建`Kotlin`中定义的FunctionalInterface的实例

```kotlin
@FunctionalInterface
interface Named {
    fun getName(): String
}
```

第一种方法，利用匿名对象:

```kotlin
val named: Named = object : Named {
    override fun getName(): String = "hello, kotlin."
}
```

其实，这种写法也不够优雅。

可以使用一个名为`Named`的方法来创建这个接口的实例。

```kotlin
@FunctionalInterface
interface Named {
    fun getName(): String
}

fun Named(lambda: (Unit) -> String): Named = object : Named {
    override fun getName(): String = lambda.invoke(Unit)
}
```

之后，就可以利用`Named`方法创建`Named`方法的实例了。

```kotlin
val named = Named { "my-name" }
```

我的经验是，最好直接使用高阶函数，而不是把FunctionalInterface当做函数的参数。一定要使用FunctionalInterface时，加上一个同名工厂函数比较好。 
