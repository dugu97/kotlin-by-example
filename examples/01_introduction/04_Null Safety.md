# Null Safety

为了消除`NullPointerException`, Kotlin中的变量类型不允许赋值为`null`。如果您需要一个可以为null的变量，通过在类型的末尾添加`?`来声明它为空。

```run-kotlin
fun main() {
//sampleStart
    var neverNull: String = "This can't be null"            // 1
    
    neverNull = null                                        // 2
    
    var nullable: String? = "You can keep a null here"      // 3
    
    nullable = null                                         // 4
    
    var inferredNonNull = "The compiler assumes non-null"   // 5
    
    inferredNonNull = null                                  // 6
    
    fun strLength(notNull: String): Int {                   // 7
        return notNull.length
    }
    
    strLength(neverNull)                                    // 8
    strLength(nullable)                                     // 9
//sampleEnd
}
```

1. 声明一个`non-null` 字符串变量。
2. 当尝试将`null`赋值给`non-null`的变量时，会产生编译错误。
3. Declares a nullable String variable.
4. 添加了`?`声明，则可以赋值为 null
5. 自动类型判断时，编译器对`用值初始化`的变量假定为 non-null。
6. 当尝试将`null`赋值给`non-null`的推断类型的变量时，会产生编译错误。
7. 声明一个带有`非空字符串`参数的函数。
8. Calls the function with a `String` (non-nullable) argument. This is OK.
9. 当用`String?`参数调用函数时，则会产生编译错误。

## Working with Nulls

有时，Kotlin程序需要处理空值，例如与外部Java代码交互或表示真正的缺失状态时。
Kotlin提供了空跟踪来优雅地处理这种情况。

```run-kotlin
//sampleStart
fun describeString(maybeString: String?): String {              // 1
    if (maybeString != null && maybeString.length > 0) {        // 2
        return "String of length ${maybeString.length}"
    } else {
        return "Empty or null string"                           // 3
    }
}
//sampleEnd

fun main() {
    println(describeString(null))
}
```

1. 接受可空字符串并返回其描述的函数。
2. If the given string is not `null` and not empty, return information about its length.
3. Otherwise, tell the caller that the string is empty or null.

    
    
