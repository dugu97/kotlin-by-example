# dynamic

*dynamic*是`Kotlin/JS`中的一种特殊类型。它基本上关闭了Kotlin的类型检查器。
为了与无类型或松散类型的环境进行互操作，这是必需的，例如
作为JavaScript生态系统。

```run-kotlin-js
fun main(){
//sampleStart
  val a: dynamic = "abc"                                               // 1
  val b: String = a                                                    // 2
  
  fun firstChar(s: String) = s[0]
  
  println("${firstChar(a)} == ${firstChar(b)}")                        // 3
  
  println("${a.charCodeAt(0, "dummy argument")} == ${b[0].toInt()}")   // 4
  
  println(a.charAt(1).repeat(3))                                       // 5
  
  fun plus(v: dynamic) = v + 2
  
  println("2 + 2 = ${plus(2)}")                                        // 6
  println("'2' + 2 = ${plus("2")}")
//sampleEnd
}
```

1. 任何值都可以分配给`dynamic`变量类型。
2. 动态值可以分配给任何变量类型。
3. 动态变量可以作为参数传递给任何函数。
4. 任何带有任何参数的属性或函数都可以在`dynamic`变量上调用。
5. 对`dynamic`变量的函数调用总是返回动态值，因此可以链接这些调用。
6. 运算符，分配和索引访问(`[..]`)均按“原样”翻译。谨防！
