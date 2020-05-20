# Smart Casts 


Kotlin编译器足够聪明，可以在大多数情况下自动执行类型转换，包括：

1. 从可为空的类型强制转换为非可为空的对应类型。
2. 从父类型转换为子类型。

```run-kotlin
import java.time.LocalDate
import java.time.chrono.ChronoLocalDate

fun main() {
//sampleStart
    val date: ChronoLocalDate? = LocalDate.now()    // 1
    
    if (date != null) {
        println(date.isLeapYear)                    // 2
    }
    
    if (date != null && date.isLeapYear) {          // 3
        println("It's a leap year!")
    }
    
    if (date == null || !date.isLeapYear) {         // 4
        println("There's no Feb 29 this year...")
    }
    
    if (date is LocalDate) {
        val month = date.monthValue                 // 5
        println(month)
    }
//sampleEnd
}

```

1. Declares a nullable variable.
2. 自动转换为`non-nullable`（因此可以直接访问`isLeapYear`）。
3. 在条件内进行自动转换（这是可能的，因为像Java一样，Kotlin使用[short-circuiting(短路)](https://en.wikipedia.org/wiki/Short-circuit_evaluation)).
4. 在条件内进行自动转换（也可通过`short-circuiting(短路)`启用）
5. 自动转换到子类型“ LocalDate”。

这样，您可以在大多数情况下根据需要自动使用变量，而无需手动进行明显的强制转换。