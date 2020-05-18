# Ranges

Kotlin中有一组用于定义范围的工具。让我们简要地看一下它们。

```run-kotlin
fun main() {
//sampleStart
    for(i in 0..3) {             // 1
        print(i)
    }
    print(" ")

    for(i in 2..8 step 2) {      // 2
        print(i)
    }
    print(" ")

    for (i in 3 downTo 0) {      // 3
        print(i)
    }
    print(" ")

//sampleEnd
}
```

1. 在0到3（包括3）之间的范围内进行迭代。
2. 使用自定义增量步长对连续元素进行遍历。
5. 以_reverse(相反)_顺序遍历一个范围。

字符范围也受支持：

```run-kotlin
fun main() {
//sampleStart
    for (c in 'a'..'d') {        // 1
        print(c)
    }
    print(" ")

    for (c in 'z' downTo 's' step 2) { // 2
        print(c)
    }
    print(" ")

//sampleEnd
}
```

1. 以字母顺序遍历char范围。
2. 字符范围也支持`step`和`downTo`。

范围在`if`语句中也很有用：

```run-kotlin
fun main() {
//sampleStart
    val x = 2
    if (x in 1..5) {            // 1
        print("x is in range from 1 to 5")
    }
    println()

    if (x !in 6..10) {          // 2
        print("x is not in range from 6 to 10")
    }
//sampleEnd
}
```

1. Checks if a value is in the range.
2. `!in`与`in`相反。
