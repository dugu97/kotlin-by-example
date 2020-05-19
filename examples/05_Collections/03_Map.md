# Map

A [map](https://kotlinlang.org/docs/reference/collections.html) map是键/值对的集合，其中每个键都是唯一的，并用于检索对应的值。为了创建地图，有`mapOf()`和`mutableMapOf()`函数。`mutableMap`的只读视图可以通过将其转换为`Map`来获得。

```run-kotlin
const val POINTS_X_PASS: Int = 15
val EZPassAccounts: MutableMap<Int, Int> = mutableMapOf(1 to 100, 2 to 100, 3 to 100)   // 1
val EZPassReport: Map<Int, Int> = EZPassAccounts                                        // 2

fun updatePointsCredit(accountId: Int) {
    if (EZPassAccounts.containsKey(accountId)) {                                        // 3
        println("Updating $accountId...")                                               
        EZPassAccounts[accountId] = EZPassAccounts.getValue(accountId) + POINTS_X_PASS  // 4
    } else {
        println("Error: Trying to update a non-existing account (id: $accountId)")
    } 
}

fun accountsReport() {
    println("EZ-Pass report:")
    EZPassReport.forEach {                                                              // 5
        k, v -> println("ID $k: credit $v")
    }
}

fun main() {
    accountsReport()                                                                    // 6
    updatePointsCredit(1)                                                               // 7
    updatePointsCredit(1)                                                               
    updatePointsCredit(5)                                                               // 8 
    accountsReport()                                                                    // 9
}
```

1. Creates a mutable `Map`.
2. Creates a read-only view of the `Map`.
3. Checks if the `Map`'s key exists.
4. Reads the corresponding value and increments it with a constant value.
5. Iterates immutable `Map` and prints key/value pairs.
6. Reads the account points balance, before updates.
7. Updates an existing account two times.
8. Tries to update a non-existing account: prints an error message. 
9. Reads the account points balance, after updates.
