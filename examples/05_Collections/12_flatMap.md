# flatMap

`flatMap` 将集合的每个元素转换为可迭代的对象，并构建基于转换结果的单个列表。转换是用户自定义的。

```run-kotlin
fun main() {

//sampleStart
    val numbers = listOf(1, 2, 3)                        // 1

    val tripled = numbers.flatMap { listOf(it, it, it) } // 2
//sampleEnd

    println("Numbers: $numbers")
    println("Transformed: $tripled")
}
```

1. Defines a collection of numbers.
2. 建立一个列表，其中每个集合元素都重复三遍。重要的是，它**不是**列表嵌套；这是一个有九个元素的整数列表。 
