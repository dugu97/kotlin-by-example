# Named Arguments

与大多数其他编程语言（Java，C ++等）一样，Kotlin支持根据定义的顺序将参数传递给方法和构造函数。
Kotlin还支持[named arguments](https://kotlinlang.org/docs/reference/functions.html#named-arguments)，以实现更清晰的调用并避免参数顺序出错。这样的错误很难找到，因为例如两个连续的参数具有相同的类型时，编译器就不会检测到它们。

```run-kotlin
fun format(userName: String, domain: String) = "$userName@$domain"

fun main() {
//sampleStart
    println(format("mario", "example.com"))                         // 1
    println(format("domain.com", "username"))                       // 2
    println(format(userName = "foo", domain = "bar.com"))           // 3
    println(format(domain = "frog.com", userName = "pepe"))         // 4
//sampleEnd
}
```

1. Calls a function with argument values.
2. Calls a function with switched arguments. No syntax errors, but the result _domain.com@username_ is incorrect.
3. Calls a function with named arguments.   
4. When invoking a function with named arguments, you can specify them in any order you like.
