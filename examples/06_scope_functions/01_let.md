# let

Kotlin标准库函数`let`可用于`作用域`和`null检查`。当调用一个对象时，`let`执行给定的代码块并返回其最后一个表达式的结果。
通过引用`it`可在块内部访问该对象。

```run-kotlin
fun customPrint(s: String) {
    print(s.toUpperCase())
}

fun main() {
//sampleStart
    val empty = "test".let {               // 1
        customPrint(it)                    // 2
        it.isEmpty()                       // 3
    }
    println(" is empty: $empty")


    fun printNonNull(str: String?) {
        println("Printing \"$str\":")

        str?.let {                         // 4
            print("\t")
            customPrint(it)
            println()
        }
    }
    printNonNull(null)
    printNonNull("my string") 
//sampleEnd
}
```

1. Calls the given block on the result on the string "_test_".
2. Calls the function on "_test_" by the `it` reference.
3. `let` returns the value of this expression.
4. 使用安全调用，因此`let`及其代码块将仅在`non-null`值上执行。
