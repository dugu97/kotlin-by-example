# sorted

`sorted` 返回一个按照自然排序顺序(升序)的列表

`sortedBy` 根据`specified selector function的返回值`的自然排序顺序对元素进行排序。

```run-kotlin
fun main() {

//sampleStart
    val shuffled = listOf(5, 4, 2, 1, 3)     // 1
    val natural = shuffled.sorted()          // 2
    val inverted = shuffled.sortedBy { -it } // 3
//sampleEnd

    println("Shuffled: $shuffled")
    println("Natural order: $natural")
    println("Inverted natural order: $inverted")
}
```

1. Defines a collection of shuffled numbers.
2. Sorts it in the natural order.
2. 通过使用`-it`作为选择器函数，以自然倒序对其进行排序。特别注意，此处的`-it`并不是指变为负数，而是修饰两个元素之间的先后排序条件
