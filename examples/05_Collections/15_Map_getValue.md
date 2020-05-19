# Map Element Access

当应用于地图时，`[]`运算符返回对应于给定键的值，如果map中没有这样的键，则返回`null`。

`getValue` 函数返回与给定键对应的现有值，如果键不存在，则抛出异常。
对于用`withDefault`创建的map, `getValue` 返回默认值，而不是抛出异常。

```run-kotlin
fun main(args: Array<String>) {

//sampleStart
    val map = mapOf("key" to 42)
    
    val value1 = map["key"]                                     // 1
    val value2 = map["key2"]                                    // 2

    val value3: Int = map.getValue("key")                       // 1

    val mapWithDefault = map.withDefault { k -> k.length }
    val value4 = mapWithDefault.getValue("key2")                // 3
    
    try {
        map.getValue("anotherKey")                              // 4
    } catch (e: NoSuchElementException) {
        println("Message: $e")
    }

//sampleEnd

    println("value1 is $value1")
    println("value2 is $value2")
    println("value3 is $value3")
    println("value4 is $value4")
}
```

1. Returns 42 because it's the value corresponding to the key `"key"`.
2. Returns `null` because `"key2"` is not in the map.
3. 返回默认值，因为不存在`key2`。所以对于这个key，默认值为4。`map.withDefault { k -> k.length }`表达的意思是默认值为key的长度。
4. Throws `NoSuchElementException` because `"anotherKey"` is not in the map.
