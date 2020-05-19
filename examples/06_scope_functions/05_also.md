# also

`also` works like [`apply`](04_apply): 它执行给定的块并返回被调用的对象。
在该块内部，该对象由`it`引用，因此更容易将其作为参数传递。
此功能非常适合嵌入其他操作，例如调用时打印日志等

```run-kotlin
data class Person(var name: String, var age: Int, var about: String) {
             constructor() : this("", 0, "")
}
         
fun writeCreationLog(p: Person) {
    println("A new person ${p.name} was created.")              
}
         
fun main() {
//sampleStart
    val jake = Person("Jake", 30, "Android developer")   // 1
        .also {                                          // 2 
            writeCreationLog(it)                         // 3
    }
//sampleEnd
}
```

1. Creates a `Person()` object with the given property values.
2. Applies the given code block to the object. The return value is the object itself. 
3. 调用将`该对象`作为参数传递的日志记录函数。
