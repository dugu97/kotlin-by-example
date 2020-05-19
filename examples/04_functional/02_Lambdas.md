# Lambda Functions

[*Lambda functions*](https://kotlinlang.org/docs/reference/lambdas.html) ("lambdas")是临时创建函数的简单方法。由于类型推断和隐式的`it`变量，在很多情况下可以非常简洁地表示Lambda。

```run-kotlin
fun main() {
//sampleStart
    // 所有示例都创建一个转换大写的函数对象。
    // 所以这是一个从String到String的函数

    val upperCase1: (String) -> String = { str: String -> str.toUpperCase() } // 1

    val upperCase2: (String) -> String = { str -> str.toUpperCase() }         // 2

    val upperCase3 = { str: String -> str.toUpperCase() }                     // 3

    // val upperCase4 = { str -> str.toUpperCase() }                          // 4

    val upperCase5: (String) -> String = { it.toUpperCase() }                 // 5

    val upperCase6: (String) -> String = String::toUpperCase                  // 6

    println(upperCase1("hello"))
    println(upperCase2("hello"))
    println(upperCase3("hello"))
    println(upperCase5("hello"))
    println(upperCase6("hello"))
//sampleEnd
}
```

1. Lambda的所有特性中,还包含随处的显式类型. lambda是花括号中的部分，花括号被分配给类型为 `(String) -> String` (a function type)的变量.
2. lambda内部的类型推断：lambda参数的类型从`为其分配的变量`的类型推断。
3. lambda之外进行类型推断：从`lambda参数的类型`和`返回值推断变量`的类型。
4. 您不能一起做(指的是`2`和`3`)，编译器没有机会以这种方式推断类型。
5. 对于具有单个参数的lambda，您不必显式命名它。相反，您可以使用隐式的`it`变量。当可以推断出`it`的类型（通常是这种情况）时，这尤其有用。
6. 如果lambda由单个函数调用组成，则可以使用函数指针（`::`）。
