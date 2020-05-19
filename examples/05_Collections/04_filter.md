# filter

*filter* 过滤器功能使您可以过滤集合。它使用一个过滤谓词作为lambda参数。谓词应用于每个元素。构成谓词`true`的元素将在结果集合中返回。

```run-kotlin
fun main() {

//sampleStart
    val numbers = listOf(1, -2, 3, -4, 5, -6)      // 1
    
    val positives = numbers.filter { x -> x > 0 }  // 2
    
    val negatives = numbers.filter { it < 0 }      // 3
//sampleEnd

    println("Numbers: $numbers")
    println("Positive Numbers: $positives")
    println("Negative Numbers: $negatives")
}
```

1. Defines collection of numbers.
2. 获取正数。
3. 使用较短的`it`表示法来获取负数
