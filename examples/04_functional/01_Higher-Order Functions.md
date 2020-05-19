# Higher-Order Functions(高阶函数)

[*高阶函数*](https://kotlinlang.org/docs/reference/lambdas.html) 是一个将另一个函数作为参数 and/or 返回一个函数的函数。

### Taking Functions as Parameters

```run-kotlin
fun calculate(x: Int, y: Int, operation: (Int, Int) -> Int): Int {  // 1
    return operation(x, y)                                          // 2
}

fun sum(x: Int, y: Int) = x + y                                     // 3

fun main() {
    val sumResult = calculate(4, 5, ::sum)                          // 4
    val mulResult = calculate(4, 5) { a, b -> a * b }               // 5
    println("sumResult $sumResult, mulResult $mulResult")
}
```

1. 声明一个高阶函数. 它接受两个整数参数，`x`和`y`. 另外，它使用另一个函数`operation`作为参数。声明中还定义了`operation`参数和返回类型。
2. 高阶函数使用提供的参数返回`operation`调用的结果。
3. 声明一个与`operation`signature匹配的函数。
4. 调用传递两个整数值和函数参数`:: sum`的高阶函数。 `::`是在Kotlin中按名称引用函数的表示法。
5. 调用传入lambda作为函数参数的高阶函数。看起来更清晰，不是吗？

### Returning Functions

```run-kotlin
fun operation(): (Int) -> Int {                                     // 1
    return ::square
}

fun square(x: Int) = x * x                                          // 2

fun main() {
    val func = operation()                                          // 3
    println(func(2))                                                // 4
}
```

1. 声明一个返回函数的高阶函数。
2. Declares a function matching the signature.
3. 调用`operation`以将结果分配给变量。在这里，`func`变成`square`，由`operation`返回.
4. 调用`func`, 实际上执行的是`Square`函数。

