# getOrElse

`getOrElse` 提供对集合元素的安全访问。它需要一个索引和一个函数(提供默认值)，以在索引超出范围时提供默认值。

```run-kotlin
fun main() {

//sampleStart
    val list = listOf(0, 10, 20)
    println(list.getOrElse(1) { 42 })    // 1
    println(list.getOrElse(10) { 42 })   // 2
//sampleEnd
}
```

1. Prints the element at the index `1`.
2. Prints `42` because the index `10` is out of bounds. 

`getOrElse`还可以应用于`Map`以获得给定键的值。

```run-kotlin
fun main() {

//sampleStart
    val map = mutableMapOf<String, Int?>()
    println(map.getOrElse("x") { 1 })       // 1
    
    map["x"] = 3
    println(map.getOrElse("x") { 1 })       // 2
    
    map["x"] = null
    println(map.getOrElse("x") { 1 })       // 3
//sampleEnd
}
```

1. Prints the default value because the key `"x"` is not in the map.
2. Prints `3`, the value for the key `"x"`.
3. 打印默认值，因为未定义键`"x"`的值。
