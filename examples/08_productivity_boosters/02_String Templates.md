# String Templates

[String templates](https://kotlinlang.org/docs/reference/basic-types.html#string-templates) 允许您将变量引用和表达式包含在字符串中。当请求字符串的值时（例如，通过`println`），所有引用和表达式都将替换为实际值。

```run-kotlin
fun main() {
//sampleStart
    val greeting = "Kotliner"
    
    println("Hello $greeting")                  // 1 
    println("Hello ${greeting.toUpperCase()}")  // 2
//sampleEnd
}
```

1. Prints a string with a variable reference. References in strings start with `$`.
2. Prints a string with an expression. Expressions start with `$` and are enclosed in curly braces.

