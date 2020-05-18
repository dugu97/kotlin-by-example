# Functions

### Default Parameter Values and Named Arguments

```run-kotlin
fun printMessage(message: String): Unit {                               // 1
    println(message)
}

fun printMessageWithPrefix(message: String, prefix: String = "Info") {  // 2
    println("[$prefix] $message")
}

fun sum(x: Int, y: Int): Int {                                          // 3
    return x + y
}

fun multiply(x: Int, y: Int) = x * y                                    // 4

fun main() {
    printMessage("Hello")                                               // 5                    
    printMessageWithPrefix("Hello", "Log")                              // 6
    printMessageWithPrefix("Hello")                                     // 7
    printMessageWithPrefix(prefix = "Log", message = "Hello")           // 8
    println(sum(1, 2))                                                  // 9
}
```

1. A simple function that takes a parameter of type `String` and returns `Unit` (i.e., no return value).
2. A function that takes a second [optional parameter with default value](https://kotlinlang.org/docs/reference/functions.html#default-arguments) `Info`. The return type is omitted, meaning that it's actually `Unit`.
3. A function that returns an integer.
4. A single-expression function that returns an integer (inferred).
5. Calls the first function with the argument `Hello`.
6. Calls the function with two parameters, passing values for both of them.
7. Calls the same function omitting the second one. The default value `Info` is used. 
8. Calls the same function using [named arguments](https://kotlinlang.org/docs/reference/functions.html#named-arguments) and changing the order of the arguments.
9. Prints the result of a function call.

### Infix Functions

Member functions and extensions with a single parameter can be turned into [infix functions](https://kotlinlang.org/docs/reference/functions.html#infix-notation).

```run-kotlin
fun main() {

  infix fun Int.times(str: String) = str.repeat(this)        // 1
  println(2 times "Bye ")                                    // 2

  val pair = "Ferrari" to "Katrina"                          // 3
  println(pair)

  infix fun String.onto(other: String) = Pair(this, other)   // 4
  val myPair = "McLaren" onto "Lucas"
  println(myPair)

  val sophia = Person("Sophia")
  val claudia = Person("Claudia")
  sophia likes claudia                                       // 5
}

class Person(val name: String) {
  val likedPeople = mutableListOf<Person>()
  infix fun likes(other: Person) { likedPeople.add(other) }  // 6
}
```

1. 定义`Int`上的中缀扩展函数。
2. 调用中缀函数。
3. 通过从标准库中调用中缀函数`to`来创建`Pair`。
4. 自定义`onto`中缀函数来实现`to`函数的功能
5. 中缀表示法也适用于对象里面函数(方法)。
6. 所处的对象或者类 即是 中缀 第一个参数（即调用方）。

Note that the example uses [local functions](https://kotlinlang.org/docs/reference/functions.html#local-functions) (functions nested within another function).

### Operator Functions

某些中缀扩展函数可以“升级”运算符层面 [operators](https://kotlinlang.org/docs/reference/operator-overloading.html), allowing their calls with the corresponding operator symbol.

```run-kotlin
fun main() {
//sampleStart
  operator fun Int.times(str: String) = str.repeat(this)       // 1
  println(2 * "Bye ")                                          // 2

  operator fun String.get(range: IntRange) = substring(range)  // 3
  val str = "Always forgive your enemies; nothing annoys them so much."
  println(str[0..14])                                          // 4
//sampleEnd
}
```

1. 使用 `operator` 进一步修饰上述中缀函数，以升级到运算符层面r
2. `times()`的操作符符号是`*` ，因此可以使用`2 * "Bye"`调用该函数。
3. 运算符函数允许对字符串进行简单的范围访问。
4. `get()`操作符启用了 [bracket-access syntax](https://kotlinlang.org/docs/reference/operator-overloading.html#indexed)语法.

### Functions with `vararg` Parameters

[Varargs](https://kotlinlang.org/docs/reference/functions.html#variable-number-of-arguments-varargs) allow you to pass any number of arguments by separating them with commas.

```run-kotlin
fun main() {
//sampleStart
    fun printAll(vararg messages: String) {                            // 1
        for (m in messages) println(m)
    }
    printAll("Hello", "Hallo", "Salut", "Hola", "你好")                 // 2
    
    fun printAllWithPrefix(vararg messages: String, prefix: String) {  // 3
        for (m in messages) println(prefix + m)
    }
    printAllWithPrefix(
            "Hello", "Hallo", "Salut", "Hola", "你好",
            prefix = "Greeting: "                                          // 4
    )

    fun log(vararg entries: String) {
        printAll(*entries)                                             // 5
    }
//sampleEnd
}
```

1. 可变参数修饰符（`vararg`）将参数转换为 `vararg`.
2. 这允许使用 任意数量 的字符串参数调用`printAll`.
3. 由于可以命名参数，您甚至可以在vararg之后添加另一个相同类型的参数。这在Java中是不允许的，因为没有传递值的方法.
4. 使用命名参数，可以给 prefix 独立设值，区别开vararg修饰的参数.
5. 在运行时，entries只是一个数组。如果要将它传递给vararg参数，可以使用特殊的拓展操作符 * ，它允许您传递 *entries(字符串的vararg)，而不是entries(数组<String>)。通俗来说，就是以字符串的形式传递，而不是以数组的形式
