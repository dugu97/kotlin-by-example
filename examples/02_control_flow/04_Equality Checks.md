# Equality Checks

Kotlin使用`==`进行结构比较，使用'===`进行引用比较。

More precisely, `a == b` compiles down to `a == null ? b == null : a.equals(b)`.

```run-kotlin
fun main(args: Array<String>) {
//sampleStart

  val authors = setOf("Shakespeare", "Hemingway", "Twain")
  val writers = setOf("Twain", "Shakespeare", "Hemingway")

  println(authors == writers)   // 1
  println(authors === writers)  // 2
//sampleEnd
}
```

1. 返回true，因为它调用authors.equals（writers）并且set数据结构是忽略元素顺序的。
2. 返回“ false”，因为“ authors”和“ writers”是不同的引用。
