# zip

`zip`函数将两个给定的集合合并为一个新的集合。默认情况下，结果集合包含具有相同索引的`Pairs`源集合元素。但是，您可以定义结果收集元素的自身结构。

结果集合的大小等于源集合的最小大小。

```run-kotlin
fun main() {

//sampleStart
    val A = listOf("a", "b", "c")                  // 1
    val B = listOf(1, 2, 3, 4)                     // 1

    val resultPairs = A zip B                      // 2
    val resultReduce = A.zip(B) { a, b -> "$a$b" } // 3
//sampleEnd

    println("A to B: $resultPairs")
    println("\$A\$B: $resultReduce")
//运行结果如下:
//A to B: [(a, 1), (b, 2), (c, 3)]
//$A$B: [a1, b2, c3]

}
```

1. Defines two collections.
2. 将它们合并成对形成一个列表。 此处使用中缀符号。
3. 通过给定的转换将它们合并为`String`列表。
