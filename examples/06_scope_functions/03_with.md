

# with

`with`是一个`non-extension`函数，可以简洁地访问其参数的成员：在引用其成员时，可以省略实例名称。

```run-kotlin
class Configuration(var host: String, var port: Int) 

fun main() {
    val configuration = Configuration(host = "127.0.0.1", port = 9000) 

//sampleStart
    with(configuration) {
        println("$host:$port")
    }

    // instead of:
    println("${configuration.host}:${configuration.port}")    
//sampleEnd
}
```
