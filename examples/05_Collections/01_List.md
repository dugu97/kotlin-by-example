# List

A [list](https://kotlinlang.org/docs/reference/collections.html)列表是项目的有序集合。在Kotlin中，列表可以是可变的(`MutableList`)或只读的(`List`)。对于列表创建，将标准库函数`listOf()`用于只读列表，将`mutableListOf()`用于可变列表。为了防止不必要的修改，请通过将可变列表转换为List来获取可变列表的只读视图。

```run-kotlin
val systemUsers: MutableList<Int> = mutableListOf(1, 2, 3)        // 1
val sudoers: List<Int> = systemUsers                              // 2

fun addSudoer(newUser: Int) {                                     // 3
    systemUsers.add(newUser)                      
}

fun getSysSudoers(): List<Int> {                                  // 4
    return sudoers
}

fun main() {
    addSudoer(4)                                                  // 5 
    println("Tot sudoers: ${getSysSudoers().size}")               // 6
    getSysSudoers().forEach {                                     // 7
        i -> println("Some useful info on user $i")
    }
    // getSysSudoers().add(5) <- Error!                           // 8
}
```

1. Creates a `MutableList`.
2. Creates a read-only view of the list.
3. Adds a new item to the `MutableList`.
4. A function that returns an read-only `List`.
5. 更新`MutableList`。由于所有相关的只读视图都指向同一对象,因此它们也会更新。
6. Retrieves the size of the read-only list.
7. Iterates the list and prints its elements.
8. Attempting to write to the read-only view causes a compilation error.
