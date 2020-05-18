# Conditional Expression

Kotlin没有三元运算符 `condition ? then : else`. 而是把`if`可以用作表达式：

```run-kotlin
fun main() {
//sampleStart
    fun max(a: Int, b: Int) = if (a > b) a else b         // 1

    println(max(99, -42))
//sampleEnd
}
```

1. if是此处的表达式：它返回一个值。
