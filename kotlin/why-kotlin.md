# 为什么我放弃了`Java`而投入`Kotlin`的怀抱

### 1. 学习成本
对于有`Java`经验的开发者来说，`Kotlin`非常易于学习。从开始学习，到正式开始用于生产环境，前后
只花费了不到一个月时间。这一个月甚至包括开发了一个玩具项目。

### 2. 语言特点
`Kotlin`是运行在JVM上语言、它是静态语言、它是强类型的、它对`null`值严格管控，使程序可大量减少
犯错。

而且`Kotlin`全完兼容`Java`的库(包括标准库和第三方库)，以前用真金白银积累的经验依然是有用的。

### 3. IDE支持
`IDEA`完美支持。

### 4. 语法特点

`Kotlin`的很多语法特性，都弥补了`Java`的不足。我们一样一样来说。

##### 4.1 多行字符串

很多语言都有多行字符串的申明语法，可惜`Java`没有。如下面的代码所示的，如果不使用多行字符串，`JPA Query Language`将特别难以阅读。如果使用`Java`编写，你会怎么做呢？用`String.format`或是用`+`拼接？恐怕你会得到一团乱麻。

```Kotlin
@Repository
open class ContactDaoImpl : ContactExtDao {

    @PersistenceContext lateinit var entityManager: EntityManager

    override fun findNewContactByUserId(userId: String): List<UserLike> {
        val ql1 = """select
                        new ${OnwerIdAndGreeting::class.java.name}(c.id.ownerId, c.greeting)
                      from
                        Contact as c
                      where
                        c.id.targetId = :userId
                      and
                        c.id.ownerId not in (select c.id.targetId from Contact as c where c.id.ownerId = :userId)
                      order by
                        c.mdate desc
                        """

        val idAndGreetings = entityManager.createQuery(ql1, OnwerIdAndGreeting::class.java)
                .setParameter("userId", userId)
                .resultList

        if (idAndGreetings.isEmpty()) {
            return listOf()
        }

        val ids = idAndGreetings.map { it.ownerId }

        val ql2 = """
                    from
                        User as u
                    where
                        u.id in :ids
                    """

        val users = entityManager.createQuery(ql2, User::class.java)
                    .setParameter("ids", ids)
                    .resultList

        return users.mapIndexed { i, user ->  UserWithGreeting(user, idAndGreetings[i].greeting)}
    }

}
```

##### 4.2 方法默认参数

在`Java`里，方法不能指定默认参数，你只好写重载函数了。

```Kotlin
fun String.equals(other: String, ignoreCase: Boolean = false)
```

##### 4.3 String格式化

上面的代码是不是要比下面的代码更简单明了？

```Kotlin
val greeting = "你好"
val world = "世界"
val s = "$greeting, $world."
```

```Java
final String greeting = "你好"
final String world = "世界"
final String s = String.format("%s, %s.", greeting, world)
```

##### 4.4 单例

`Kotlin`从语法层面支持单例这一最常用的设计模式。

```
object MySingleton {
    override fun toString() = "我是单例对象"
}
```

##### 4.5 装饰器

// TODO
