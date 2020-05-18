# Variables

Kotlin有强大的类型推断。虽然可以显式地声明变量的类型，但通常会让编译器通过推断来完成这项工作。
Kotlin并没有强制执行不变性，尽管它是推荐的。本质上还是用*val*而不是*var*。

```run-kotlin
fun main() {
//sampleStart
    var a: String = "initial"  // 1
    println(a)
    val b: Int = 1             // 2
    val c = 3                  // 3
//sampleEnd
}
```

1. 声明一个可变变量并初始化它。
2. 声明一个不可变变量并初始化它。
3. 声明一个不可变变量，并在不指定类型的情况下初始化它。编译器推断类型`Int`。

```run-kotlin
fun main() {
//sampleStart
    var e: Int  // 1
    println(e)  // 2
//sampleEnd
}
```

1. 声明一个可变变量，但不初始化它。
2. 试图使用该变量会导致编译错误: `Variable 'e' must be initialized`.

您可以自由选择何时初始化变量，但是，必须在第一次读取变量之前对其进行初始化。

```run-kotlin
fun someCondition() = true 

fun main() {
//sampleStart
    val d: Int  // 1
    
    if (someCondition()) {
        d = 1   // 2
    } else {
        d = 2   // 2
    }
    
    println(d) // 3
//sampleEnd
}
```

1. 声明一个没有初始化的不可变变量。
2. 根据某些条件，使用不同的值初始化变量。
3. 读取变量是可能的，因为它已经被初始化了.
