# Data Classes

[Data classes](https://kotlinlang.org/docs/reference/data-classes.html) 使得创建用于存储值的类变得容易。此类自动提供了用于复制，获取字符串表示形式以及在集合中使用实例的方法。

```run-kotlin
data class User(val name: String, val id: Int)             // 1

fun main() {
    val user = User("Alex", 1)
    println(user)                                          // 2

    val secondUser = User("Alex", 1)
    val thirdUser = User("Max", 2)

    println("user == secondUser: ${user == secondUser}")   // 3
    println("user == thirdUser: ${user == thirdUser}")

    println(user.hashCode())                               // 4
    println(thirdUser.hashCode())

    // copy() function
    println(user.copy())                                   // 5
    println(user.copy("Max"))                              // 6
    println(user.copy(id = 2))                             // 7
    
    println("name = ${user.component1()}")                 // 8
    println("id = ${user.component2()}")
}
```

1. 用`data`修饰符定义一个数据类。
2. 方法`toString`是自动生成的，这使得`println`的输出看起来不错。
3. 自动生成的`equals`如果两个实例的所有属性都相等，则认为它们相等。
4. 相等的数据类实例具有相同的`hashCode（）`.
5. 自动生成的“复制”功能使创建新实例变得容易。
6. 复制时，您可以更改某些属性的值。 `copy`以与类构造函数相同的顺序接受参数。
7. Use `copy` with named arguments to change the value despite of the properties order.
8. 自动生成的`componentN`函数使您可以按声明的顺序获取属性的值
