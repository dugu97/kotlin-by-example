# partition

`partition` 函数使用给定的谓词将`原始集合`拆分为`成对的列表`：分别为
 * 谓词为`true`的元素.
 * 谓词为`false`的元素.

```run-kotlin
fun main() {

//sampleStart
    val numbers = listOf(1, -2, 3, -4, 5, -6)                // 1
    
    val evenOdd = numbers.partition { it % 2 == 0 }           // 2
    val (positives, negatives) = numbers.partition { it > 0 } // 3
//sampleEnd

    println("Numbers: $numbers")
    println("Even numbers: ${evenOdd.first}")
    println("Odd numbers: ${evenOdd.second}")
    println("Positive numbers: $positives")
    println("Negative numbers: $negatives")
}

//运行结果如下:
//Numbers: [1, -2, 3, -4, 5, -6]
//Even numbers: [-2, -4, -6]
//Odd numbers: [1, 3, 5]
//Positive numbers: [1, 3, 5]
//Negative numbers: [-2, -4, -6]
```

1. Defines a collection of numbers.
2. Splits `numbers` into a `Pair` of lists with even and odd numbers.
3. Splits `numbers` into two lists with positive and negative numbers. 在这里应用Pair destructuring来获取`Pair`成员。
