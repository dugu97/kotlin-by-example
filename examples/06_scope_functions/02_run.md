# run

类似 [`let`](01_let), `run`是标准库中的另一个作用域函数。基本上，它执行相同的操作：执行代码块并返回其结果。
区别在于，在`run`内部，对象通过`this`访问。当您要调用对象的方法而不是将其作为参数传递时，这很有用。

```run-kotlin

fun main() {
//sampleStart
    fun getNullableLength(ns: String?) {
        println("for \"$ns\":")
        ns?.run {                                                  // 1
            println("\tis empty? " + isEmpty())                    // 2
            println("\tlength = $length")                           
            length                                                 // 3
        }
    }
    getNullableLength(null)
    getNullableLength("")
    getNullableLength("some string with Kotlin")
//sampleEnd
}
```

1. Calls the given block on a nullable variable.
2. Inside `run`, the object's members are accessed without its name.
3. 如果不是`null`，则`run`会返回给定`String`的`length`。     
