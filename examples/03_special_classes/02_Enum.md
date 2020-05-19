# Enum Classes

[Enum classes](https://kotlinlang.org/docs/reference/enum-classes.html) 用于对表示有限的一组不同值的类型进行建模，例如方向，状态，模式等。

```run-kotlin
enum class State {
    IDLE, RUNNING, FINISHED                           // 1
}

fun main() {
    val state = State.RUNNING                         // 2
    val message = when (state) {                      // 3
        State.IDLE -> "It's idle"
        State.RUNNING -> "It's running"
        State.FINISHED -> "It's finished"
    }
    println(message)
}

```

1. 用三个枚举实例定义一个简单的枚举类。实例的数量始终是有限的，并且它们都是不同的。
2. 通过类名称访问枚举实例。
3. 使用枚举，编译器可以推断出`when`-expression是否全面，因此您不需要`else`-case。

枚举可能包含与其他类一样的属性和方法，用分号将其与实例列表分开

```run-kotlin

enum class Color(val rgb: Int) {                      // 1
    RED(0xFF0000),                                    // 2
    GREEN(0x00FF00),
    BLUE(0x0000FF),
    YELLOW(0xFFFF00);

    fun containsRed() = (this.rgb and 0xFF0000 != 0)  // 3
}

fun main() {
    val red = Color.RED
    println(red)                                      // 4
    println(red.containsRed())                        // 5
    println(Color.BLUE.containsRed())                 // 6
}

```

1. 定义带有属性和方法的枚举类。
2. 每个实例必须为构造函数参数传递一个参数。
3. 枚举类成员与实例定义之间用分号分隔。
4. The default `toString` returns the name of the instance, here `"RED"`.
5. 在枚举实例上调用方法。
6. 通过枚举类名称调用方法。
