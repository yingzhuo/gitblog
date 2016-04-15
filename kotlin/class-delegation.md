# 对象代理

```kotlin
interface MyInterface {
    fun method1(): Unit
    fun method2(): Unit
    fun method3(): Unit
}

object MyInterfaceDefault : MyInterface {
    override fun method1(): { println("method1") }
    override fun method2(): { println("method2") }
    override fun method3(): { println("method3") }
}

class MyInterfaceWrapper(val inner: MyInterface) : MyInterface by inner {
    override fun method2(): {
        inner.method2()
        println("another method2")
    }
}

fun main(args: Array<String>) {
    val i = MyInterfaceWrapper(MyInterfaceDefault)

    i.method1()
    i.method2()
    i.method3()
}
```

用这样的技术实现装饰器模式很方便。
