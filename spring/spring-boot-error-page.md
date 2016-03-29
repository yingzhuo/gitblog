# SpringBoot配置错误页面

**以配置404页面为例**

配置错误页面: (kotlin)

```kotlin
import org.springframework.boot.context.embedded.ConfigurableEmbeddedServletContainer
import org.springframework.boot.context.embedded.EmbeddedServletContainerCustomizer
import org.springframework.boot.context.embedded.ErrorPage
import org.springframework.context.annotation.Bean
import org.springframework.context.annotation.Configuration
import org.springframework.http.HttpStatus

@Configuration
open class ApplicationCnfServer {

    @Bean
    open fun errorPageCusomizer(): EmbeddedServletContainerCustomizer {
        return EmbeddedServletContainerCustomizer { container: ConfigurableEmbeddedServletContainer ->
            container.addErrorPages(ErrorPage(HttpStatus.NOT_FOUND, "/error/404"))
        }
    }

}
```

配置ErrorController: (kotlin)

```kotlin
import org.springframework.http.HttpStatus
import org.springframework.http.ResponseEntity
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RestController

@RestController
@RequestMapping("error")
open class ErrorController {

    @RequestMapping("404")
    open fun _404(): ResponseEntity<Json> {
        return Json.create(HttpStatus.NOT_FOUND).asResponseEntity()
    }

}
```

工具类Json: (kotlin)


```kotlin
import com.fasterxml.jackson.annotation.JsonIgnore
import org.springframework.http.HttpHeaders
import org.springframework.http.HttpStatus
import org.springframework.http.MediaType
import org.springframework.http.ResponseEntity
import java.io.Serializable

class Json private constructor() : Iterable<Map.Entry<String, Any?>>, Serializable {

    companion object {
        private val JSON_HTTP_HEADERS: HttpHeaders by lazy {
            val headers = HttpHeaders()
            headers.contentType = MediaType.APPLICATION_JSON_UTF8
            headers.set("Pragma", "No-cache")
            headers.set("Cache-Control", "No-cache")
            headers.setDate("Expires", 0)
            return@lazy HttpHeaders.readOnlyHttpHeaders(headers)
        }

        fun create(status: HttpStatus = HttpStatus.OK, error: String? = null): Json = Json().status(status).error(error)
    }

    var status: Int = 200
    var error: String? = null
    val payload: MutableMap<String, Any?> = mutableMapOf()
    val size: Int get() = payload.size
    val empty: Boolean get() = payload.isEmpty()

    @get:JsonIgnore
    val notEmpty: Boolean get() = !empty

    fun status(status: HttpStatus): Json = status(status.value())

    private fun status(status: Int): Json {
        this.status = status
        return this
    }

    fun error(error: String?): Json {
        this.error = error
        return this
    }

    fun put(pair: Pair<String, Any?>): Json {
        val (k, v) = pair
        this.payload[k] = v
        return this
    }

    fun put(vararg pairs: Pair<String, Any?>): Json {
        for (pair in pairs) {
            put(pair)
        }
        return this
    }

    fun clear(): Json {
        payload.clear()
        return this
    }

    fun containsKey(payloadKey: String): Boolean {
        if (empty) return false
        return payload.containsKey(payloadKey)
    }

    override fun iterator(): Iterator<Map.Entry<String, Any?>> {
        return this.payload.iterator()
    }

    fun asResponseEntity(): ResponseEntity<Json> {
        return ResponseEntity(this, JSON_HTTP_HEADERS, HttpStatus.valueOf(this.status))
    }
}
```
