# find, findLast

`find` and `findLast` 函数返回与给定谓词匹配的第一个或最后一个集合元素。如果没有这样的元素，则函数返回`null`。


```run-kotlin
fun main() {

//sampleStart
    val words = listOf("Lets", "find", "something", "in", "collection", "somehow")  // 1
    
    val first = words.find { it.startsWith("some") }                                // 2
    val last = words.findLast { it.startsWith("some") }                             // 3
    
    val nothing = words.find { it.contains("nothing") }                             // 4
//sampleEnd

    println("The first word starting with \"some\" is \"$first\"")
    println("The last word starting with \"some\" is \"$last\"")
    println("The first word containing \"nothing\" is ${nothing?.let { "\"$it\"" } ?: "null"}")
}
```

1. Defines a collection of words.
2. Looks for the first word starting with "some".
3. Looks for the last word starting with "some".
4. Looks for the first word containing "nothing".
