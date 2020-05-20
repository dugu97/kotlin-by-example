# Destructuring Declarations

[Destructuring declaration](https://kotlinlang.org/docs/reference/multi-declarations.html#destructuring-declarations) 结构声明语法非常方便，尤其是当您仅需要一个实例来访问其成员时。它使您可以定义实例而无需使用特定名称，从而节省了几行代码。

```run-kotlin
fun findMinMax(list: List<Int>): Pair<Int, Int> { 
    // do the math
    return Pair(50, 100) 
}

fun main() {
//sampleStart
    val (x, y, z) = arrayOf(5, 10, 15)                              // 1

    val map = mapOf("Alice" to 21, "Bob" to 25)
    for ((name, age) in map) {                                      // 2
        println("$name is $age years old")          
    }

    val (min, max) = findMinMax(listOf(100, 90, 50, 98, 76, 83))    // 3

//sampleEnd
}
```

1. Destructures an `Array`. The number of variables on the left side matches the number of arguments on the right side.
2. Maps can be destructured as well. `name` and `age` variables are mapped to the map key and value.
3. Built-in `Pair` and `Triple` types support destructuring too, even as return values from functions.

```run-kotlin
data class User(val username: String, val email: String)    // 1

fun getUser() = User("Mary", "mary@somewhere.com")

fun main() {
    val user = getUser()
    val (username, email) = user                            // 2
    println(username == user.component1())                  // 3

    val (_, emailAddress) = getUser()                       // 4
    
}
```

1. Defines a data class.
2. Destructures an instance. Declared values are mapped to the instance fields.
3. 在解构的过程中，会调用`data class`自动生成的`component1()` 和 `component2()`方法。
4. 如果不需要这些值之一，请使用 _下划线_，以避免编译器提示指示未使用的变量

```run-kotlin
class Pair<K, V>(val first: K, val second: V) {  // 1
    operator fun component1(): K {              
        return first
    }

    operator fun component2(): V {              
        return second
    }
}

fun main() {
    val (num, name) = Pair(1, "one")             // 2

    println("num = $num, name = $name")
}
```

1. Defines a custom `Pair` class with `component1()` and `component2()` methods.
2. 与内置`Pair`相同的方式来解构此类的实例。
